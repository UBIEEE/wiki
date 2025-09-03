---
title: MicroMouse Getting Started
---

# Getting Started

Before embarking on this journey of designing a MicroMouse, we must make it clear that creating a MicroMouse is not an easy task and will require a lot of time, effort, and dedication. This warning is not meant to scare you away, just to make sure you understand what you are getting into. We recommend MicroMouse teams consist of 4 or 5 people to make the workload manageable, with each person having a specific role (e.g. mechanical, electrical, software, etc.).

It is usually a good idea to make your first MicroMouse simple. Remember, this is a club for college students, and the competitions we attend are not as competitive as the ones shown in the Veritasium video. Solving the maze, regardless of how fast you do it, will typically land you within the top 10 at most college-level competitions.

However, if you are feeling adventurous and your team members have some more electrical experience (and abundant free time), designing a custom PCB may be the route for you. Be warned, this comes with its challenges and risks, as R&D of PCBs can be very complicated and potentially quite expensive if you need to order more than one version.

With all that said, this wiki contains information relevant to both routes, with specifics intermixed when necessary.

## Creating a Proposal

Our club only has a limited budget, so we ask that your MicroMouse team create a "proposal" outlining your robot design before any parts are ordered.

Create a repository on our [GitHub organization](https://github.com/ubieee) and write your proposal in the repo's README.md file. See our [Proposal Example](https://github.com/UBIEEE/Micromouse_Proposal_Example).

Your MicroMouse proposal should include:

- A list of all parts you plan to use, including links and prices.
    - Parts may only be purchased from vendors on the [SA approved vendors list](https://safe.sa.buffalo.edu/vendors/preferred).
    - Your team's budget is flexible, but you should aim to keep your total cost around $100.
    - If you plan to use a part we already have in stock, include the part in your list but do not include a link or price.
- An electrical schematic of your robot.
    - Must show how all components are connected together and powered.
    - You can use [KiCad](https://www.kicad.org/), NI Multisim, or another schematic software to create this, or you can just draw it out by hand.
- A Hardware Plan
    - Detailed explanation of how your hardware will work. This should demonstrate that you understand the electrical requirements of all the individual components and have a solid plan for how they will all interact with each other. Creating a CAD model of your robot is recommended.
- A Software Plan
    - Detailed explanation of how your software will work. This should include the programming language(s) you will be using, any libraries, what IDE(s) you will be working with, your approach for testing your software, and how you will be using the inputs from your hardware to complete your task.
- A list of team members and their responsibilities.
    - Each team member should include a one paragraph description of their responsibilities on the MicroMouse team.
- A timeline for your project with milestones.
    - A list of important dates and what you plan to accomplish by each date.

## Designing Your MicroMouse

### Dimensional Constraints

![Maze Cell Dimensions Image](../assets/micromouse/maze-cell-dimensions-light-bg.png#only-light){ align=right  width=300 }
![Maze Cell Dimensions Image](../assets/micromouse/maze-cell-dimensions-dark-bg.png#only-dark){ align=right  width=300 }

The first thing to think about is how big your MicroMouse should be. Size will impact many future design decisions, such as which motors and sensors you use.

Each cell of the maze is 18 cm square. Each wall of the maze is 1.2 cm wide, so there is 16.8 cm of free space in between the walls. Your MicroMouse should give at least a few centimeters of clearance on each side. 

If you plan for your MicroMouse to drive diagonally between cells, it will need a width smaller than 11.8 cm. You should give a healthy amount of clearance too, since driving diagonally is much more dangerous than driving normally. The constraints for diagonal-capable robots are very difficult to work with. Don’t feel like you need to go diagonally – there are plenty of speedy MicroMouse robots that win competitions without being able to do so.

The cells are 5 cm tall, but there is no height limit for your robot.

