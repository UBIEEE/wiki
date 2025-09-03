---
title: MicroMouse Maze Solving Algorithms
---

# Maze Solving Algorithms

There exist many different maze solving strategies used by MicroMouse robots, but no established "best". The algorithm which you choose can be as simple or as complex as you want, it's up to you. In this section, I will describe some good strategies and common practices, but feel free to experiment as you wish. 

!!! note
    Do not concern yourself with optimizing your algorithm until your MicroMouse can reliably navigate the maze. Simple algorithms will go a long way. We recommend that everybody implements FloodFill first. 

At most competitions, the time of your robot's initial "search run" does not matter because only the fastest run will count. However, some competitions (notably APEC) incorporate a "search penalty" to your final score, rewarding robots that have fast initial runs. For this reason, it is usually a good idea to search efficiently on your first run to the goal. Then once your robot reaches the goal, it can take as much time as it needs to return back to the start. 

Most MicroMouse robots use the FloodFill search algorithm during their search run because of its efficiency and its simplicity. However, FloodFill search will not guarantee that your robot reveals the shortest path (distance) to the goal on its first run. Therefore, your robot must use its "travel back to the start time" to search more of the maze. There are many options for how to do this: 

1. Use FloodFill to search back to the start. After returning to the start, your robot will have revealed a large portion of the maze, and more likely than not, has revealed the shortest path to the goal. If you want to be absolutely sure that your robot has revealed the shortest path, you can run FloodFill again from the start to the goal (or from the cell directly outside the start cell to the goal, if you need to save a run).
2. Use BFS to search for the shortest path back to the start. BFS is guaranteed to find the shortest path, however it is not a very efficient algorithm because it involves lots of backtracking. Since your robot has already revealed parts of the maze on the way to the goal, you may be able to optimize BFS slightly to make it faster.
3. Use DFS or similar algorithm to explore the entire maze. Once your robot has discovered every route to the goal, it can then compute the path to take during speed runs using factors other than distance. Robots that can drive diagonally or ones that can speed up very fast during straightaways may be able to choose faster paths this way. 

## FloodFill

FloodFill is a simple search algorithm used to find the shortest path to the goal in a maze. Given a grid of cells, FloodFill will output a grid of values which represent how far away each cell is from the goal.
Navigating using FloodFill is simple: run the FloodFill algorithm with your current knowledge of the maze, and then drive your robot in the direction of the smallest value in the grid.

Below is some pseudocode for Floodfill:

```
FloodFill(endpoints) 
  V = new Int[MAZE_WIDTH_CELLS][MAZE_LENGTH_CELLS]
  V.fill(MAX_CELL_VALUE) 

  Q = new Queue<Cell> 
  Q.add(endpoints) 
   
  While (Q is not empty)
    cell = Q.pop() 
    newValue = V[cell.x][cell.y] + 1 
    Foreach (dir in { NORTH, EAST, SOUTH, WEST }) 
      If (cell.hasExit(dir))
        nextCell = cell.neighbor(dir) 
        If (V[nextCell.x][nextCell.y] > newValue) 
          V[nextCell.x][nextCell.y] = newValue 
          Q.push(nextCell) 
        End 
      End 
    End 
  End 

  return V 
End 
```

## Breadth First Search

See the [BFS Wikipedia Article](https://en.wikipedia.org/wiki/Breadth-first_search) for implementation details.

## Depth First Search

See the [DFS Wikipedia Article](https://en.wikipedia.org/wiki/Depth-first_search) for implementation details.

## Algorithm Simulation

Our [MicroMouse Simulator](https://github.com/UBIEEE/MicroMouseSimulator) program lets you test the efficiency of different algorithms quickly on randomly generated mazes before you implement and test them on your actual robot. There are already a few popular algorithms implemented in the simulator. If you want to add your own algorithm, simply create a new class inherited from `Solver` and copy how the other solver classes are added. 

Alternatively, you could also check out [mms](https://github.com/mackorone/mms), another simulator made by a former UB IEEE club member.

