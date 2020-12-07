---
layout: post
title: Reverse Engineering the StarCraft II Selection System
---

If you're unfamiliar with StarCraft II (SC2) it's a 1v1 Real-Time Strategy game that embodies the "commander" fantasy. You build up a base, an economy and an army and attempt to destroy all of your opponent's buildings.

You control **almost everything** that happens in the game (Hence, the "commander" fantasy), and that means you're going to be clicking and using your keyboard a lot. High level players (Top ~5% or above) often play at 200-300 actions per minute (4-5 actions per **second**!).

SC2 also has a powerful hotkey system and provides you with a few simple but flexible ways to manipulate selections of units and buildings. High level players frequently use these tools throughout the game to efficiently manage their resources and quickly execute tasks.

Because the game is real-time, multi-tasking is extremely important and is one of the key differences between tiers of players.

I like exploring different ways to analyze SC2 using the [replay parser](https://github.com/Zephyrblu/zephyrus-sc2-parser) I'm building, and being able to track a player's selections at every point in the game would provide a great foundation to analyze multi-tasking.

However, current implementations of selection tracking [are not perfect](https://github.com/ggtracker/sc2reader/blob/upstream/sc2reader/engine/plugins/selection.py#L9) and documentation on how replay files are structured is [practically non-existent](https://github.com/Blizzard/s2protocol/tree/master/docs) (Especially the selection system), I needed to figure out and implement this myself.

### Contents
- **How the hell does this work?**
- **It's ALIVE**
- **`def _create_bitmask` (Not fun)**

## How the hell does this work?



## It's ALIVE



## `def _create_bitmask` (Not fun)


Two types of relevant events: SSelectionDeltaEvent and SControlGroupUpdateEvent.

Examples of events:

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

We can already see that both Selection and Control Group events share a fair amount of similarities. The biggest differences are that Control Group events have update types, and Selection events have units attached to them. We'll see how these work together to create the overall system a bit later on.

The first interesting thing to note is that a player's current selection is Control Group 10. 

## Raw Selections

## Control Groups

