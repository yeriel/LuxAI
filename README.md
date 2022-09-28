# LuxAI

## Introduction

The night is dark and full of terrors. Two teams must fight off the darkness, collect resources, and advance through the ages. Daytime finds a desperate rush to gather the resources that can carry you through the impending night whilst growing your city. Plan and expand carefully -- any city that fails to produce enough light will be consumed by darkness.

The Lux AI Challenge is a competition where competitors design agents to tackle a multi-variable optimization, resource gathering, and allocation problem in a 1v1 scenario against other competitors.

## Getting Started

You will need Node.js version 12 or above. See installation instructions [here](https://nodejs.org/en/download/), you can just download the recommended version.

Open up the command line, and install the competition design with

```
npm install -g @lux-ai/2021-challenge@latest
```

You may ignore any warnings that show up, those are harmless. To run a match from the command line (CLI), simply run

```
lux-ai-2021 path/to/botfile path/to/otherbotfile
```

and the match will run with some logging and store error logs and a replay in a new errorlogs folder and replays folder. Logs stored in the errorlogs will include all error output and anything printed to standard error by your agent. You can watch the replay stored in the replays folder using the [visualizer](https://2021vis.lux-ai.org/). 

## Goal
To have the most CityTiles at the end of the game, which is determined by the win conditions. 

### Win Conditions

After 360 turns the winner is whichever team has the most CityTiles on the map. If that is a tie, then whichever team has the most units owned on the board wins. If still a tie, the game is marked as a tie.

A game may end early if a team no longer has any more Units or CityTiles. Then the other team wins.

To know the environment conditions and restrictions you saw this [link](https://www.lux-ai.org/specs-2021), along with API documentation see this [document](https://github.com/Lux-AI-Challenge/Lux-Design-2021/tree/master/kits)