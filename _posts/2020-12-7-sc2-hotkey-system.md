---
layout: post
title: Reverse Engineering the StarCraft II Hotkey System
---

----- This article is not finished yet -----

----- I need a hook -----

StarCraft II's hotkey system is one of the most useful and important parts of the entire game.

----- I need a hook -----

If you're unfamiliar with StarCraft II (SC2), it's a 1v1 Real-Time Strategy game that embodies the "commander" fantasy. You build up a base, an economy and an army and attempt to destroy all of your opponent's buildings.

Almost everything that happens in the game is your responsibility (Hence, the "commander" fantasy), and that means you're going to be clicking and using your keyboard a lot (Pros often play at **300+ actions per minute**!).

SC2 also has a powerful hotkey system and provides you with a few simple but flexible ways to manipulate selections of units and buildings.

I like exploring different ways to analyze SC2 using the [replay parser](https://github.com/Zephyrblu/zephyrus-sc2-parser) I'm building, and being able to track a player's selections at every point in the game seemed like it would provide a great foundation to analyze multi-tasking.

However, current implementations of selection tracking [are not perfect](https://github.com/ggtracker/sc2reader/blob/upstream/sc2reader/engine/plugins/selection.py#L9) and documentation on how replay files are structured is [practically non-existent](https://github.com/Blizzard/s2protocol/tree/master/docs) (Especially the selection system), I needed to figure out and implement this myself.

## How the hell does this work?

That's how I felt looking at the Selection and Control Group JSON events for the first time. At first glance it's impossible to understand how the in-game systems map to event data.

Let's back up a little bit and explain 

- Exploring events
- Verifying in replays
- Building out an understanding

Two types of relevant events: SSelectionDeltaEvent and SControlGroupUpdateEvent.

Here's a Control Group event:

```
{
    'm_controlGroupIndex': 3,                       # control group number
    'm_controlGroupUpdate': 2,                      # type of update
    'm_mask': {'Mask': (4, 12)},                    # type of selection
    '_event': 'NNet.Game.SControlGroupUpdateEvent', # type of event
    '_eventid': 29,
    '_gameloop': 985,                               # internal game time (1s = 22.4 gameloops)
    '_userid': {'m_userId': 0},                     # player id
    '_bits': 56
}
```

And a Selection event:

```
{
    'm_controlGroupId': 10,                     # control group number
    'm_delta': {
        'm_subgroupIndex': 0,
        'm_removeMask': {'ZeroIndices': []},    # type of selection
        'm_addSubgroups': [{                    # list of unit types to be added to the selection
            'm_unitLink': 107,                  # unit type id
            'm_subgroupPriority': 33,
            'm_intraSubgroupPriority': 1,
            'm_count': 1                        # number of units of this type
        }],
        'm_addUnitTags': [40370177]             # ids of all units being added
    },
    '_event': 'NNet.Game.SSelectionDeltaEvent', # type of event
    '_eventid': 28,
    '_gameloop': 1132,                          # internal game time (1s = 22.4 gameloops)
    '_userid': {'m_userId': 0},                 # player id
    '_bits': 136
}
```

## It's ALIVE

- Framework is up and running
- The system works, kind of
- Some issues...

## `def _create_bitmask` (Not fun)

- The problem
- The root cause
- Special bitmasks explained
- Previous implementation: https://github.com/ggtracker/sc2reader/blob/4c6703742094103842a9de827fd4a051e6cf7977/sc2reader/readers.py#L566-L592

## The afterlife

- What happens when a unit dies?

## A new discovery

- Control Group update type 5 (Steal and bind)
- Running the parser through thousands of pro replays to check for regressions
- Find a lot of ControlGroup errors
- Discover the new update type and quickly realize what it is
- Double check functionality in dummy replays, then implement fix
- All replays complete parsing, so can at least know that I am tracking every single selection made since there are no KeyErrors (Accessing a non-existent control group) or IndexErrors (Accessing an out-of-bounds index)!


- Still not 100% about whether the selections are always correct or not, but manually verifying selections in replays is very time consuming and not very interesting. Am relatively convinced that it's accurate, or at least accurate enough.
