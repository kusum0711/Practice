# Challenge

Welcome to the challenge!

Some packages are already being installed for you below - you can just start reading the below text while that finishes.

## The Introduction

The following script takes you through tasks you should complete as part of your challenge. Some tasks may be tricky, some may be easy. In every case you are encouraged to pose written questions to the task itself, write down questions/observations or reasoning about why you did not find a solution. In most cases though, a working solution will be achievable. In all cases it will be helpful if add notes about your methodology (e.g.: "I did X using Y because of Z, then A happened which I fixed doing B. I should have seen A coming but didn't because of C").

There will be no loop with the reviewer, so nobody is going to answer your notes, questions, musings, ... - their main aim is to showcase your thought process for a fellow developer who will inspect this challenge. For the texts you can write everything from a bullet list to a book, but be aware that in development we usually try to optimize for a combination of dense information + understandability by every team member. We firmly believe that good communication and conceptualization is as important to being a developer as the coding itself.

The challenge tries to be similar to the real-world with the kinds of problems and solutions that would occur in every-day-project-work. There will be no questions asking you to optimize runtime-complexity in O-notation to the max for algorithm Y - these sort of questions do not make any sense in our opinion. Being close to the real-world also means that you may bring in CSS/JS Libraries to help you develop, just make sure that everything still runs in stackblitz.

The tool we use here is called `stackblitz`. It functions as a fully integrated development environment (IDE). You can go through the full challenge here. If you want to use your local environment you can also download the project using the small "cloud icon" at the top left corner of the screen, just right of "Project". _In the end, the challenge code must run in here inside `stackblitz`, so `pnpm run dev` has to work. If this is not the case, we will not be able to review your challenge!_

## Tech-Stack

You can skip this section and revisit it later, as the right information will be shared with you at the right places and everything should "just work" as we inteded it to work. If you still want to learn more right now, read on!

This is a "fullstack" TypeScript project using nuxt3 + vue3. Fullstack TypeScript means that we use one typescript code base for both the backend API + the frontend webapp. We have defined helper commands for development, testing, running the app in production, linting, ... that are runnable via `pnpm run X` where X is the command, checkout the `package.json` for more.

For styling we use TailwindCSS, so far the zoo has not added a CSS component framework to use pre-made components, maybe you will? For testing we use `vitest`, for linting `eslint`.

This information will also be shared with you where needed as part of the challenge, so there is no need to dive into anything at all for now.

## The Challenge

So, without further ado: Welcome, new IT Director of the Cologne Zoo! As you can see, the zoo dashboard was badly damaged by the recent malware attacks from the Duisburg Zoo. The old IT Director quit after that attack as he just could not take it anymore. The staff is looking to you to fix this mess and bring the zoo dashboard back to its former glory! 🐻 🐵 Sadly the IT-Department has been underfunded for years before the attack - so the application is quite dated.

### Task 1: Take stock of the repository

In a first step you should inspect the health of the project and report on everything you notice while doing so. This will help you determine what repairs are necessary in the coming steps.

Please take stock fo the page using developer tools, your instincts, ... and write down below what you find.

// Your solution

1.  Issue: alert() function not available during server side rendering.
2.  Issue: ANlMALS is not defined.

### Task 2: Get the basics running again

Now that we know that is broken, let's try to get things running again, step by step. First we should aim to just get the project to start. Please fix the problem that stops `pnpm run dev` from working out. Then:

- document the loaded page with a brief description,
- document the problems that needed to be resolved to make it work (so that we can avoid and quicker fix them in the future!)

Zookeepers reported that the error sometimes changes when reloading the page after the initial start.

// Your solution
Problems that needed to be resolved:

1.  Issue: alert() function not available during server side rendering.

    - Solution: Used onMounted(() => { alert('get wrecked cologne zoo!') }) to run only on client-side
    - Location: app.vue file

2.  Issue: ANlMALS is not defined.
    - Solution: Corrected the spelling error. ANlMALS TO ANIMALS.
    - Location: animals.get.ts file

Page description after fixing:
The page loads showing "Cologne Zoo" dashboard with an overview description for zookeepers. It displays a table titled "Our (lovely) Animals:" with columns for Index, Species, Gender, Age (yrs), and Weight (kg). The table shows 50 animals with their data, currently sorted by weight.

Issues noticed on the page:

1. Missing "name" column that should be in third position
2. Age column shows timestamps/dates instead of actual age in years
3. No animal names are displayed (though defined in types)
4. height and Favourite fruit column is also missing. (though defined in types)

### Task 3: Start the documentation

You got it to work! Nice, now the basic functionality is back for the zookeepers. This would be a great point to start on documenting the project. As you can see there is not even a readme file! The old IT Director seems to have left this project in bad shape. Please add documentation with basics on the project, how to start, stop, test, ... it and whatever else information you deem important.

Add your solution below, either as an inline text or link to new documentation file(s) you've created.

// Your solution

# Cologne Zoo Dashboard

## Overview

A full-stack TypeScript application for managing zoo operations and animal data. This dashboard provides zookeepers with an overview of animals and their relevant health data. Built with modern web technologies to ensure reliability and ease of use.

## Tech Stack

- **Frontend**: Nuxt3, Vue3, TypeScript
- **Styling**: TailwindCSS
- **Testing**: Vitest
- **Linting**: ESLint
- **Package Manager**: pnpm

## Getting Started

### Prerequisites

- Node.js
- pnpm (install with `npm install -g pnpm`)

### Installation

```bash
# Clone the repository (if applicable)
# Navigate to project directory

# Install dependencies
pnpm install
```

### Development

```bash
# Start the development server
pnpm run dev
```

The application will be available at `http://localhost:3000`

### Testing

```bash
# Run all tests
pnpm run test

# Run tests in watch mode
pnpm run test:watch


```

### Task 4: Test fixing

There's a failing test that for the age calculation helper. Can you figure out what is broken in the implementation or the test it is and resolve the problem? All zookeepers are really interested in what is going on here.

// Your solution
The original code used Math.round() to calculate an animal's age. That works fine in general, but it caused a problem: if an animal was born today, the age would be 0, and Math.round(0) stays 0. However, the test expected the age to be 1.

To fix this, I made two changes:

Switched to Math.ceil() so any partial age (like 0.4) gets rounded up instead of down.

Wrapped it with Math.max(1, ...) to make sure the minimum age is always at least 1, even for newborns.

- Location : "utils/useCalculateAgeInYears.ts"

### Task 5: UI Fixing and Improvement

The zookeepers report that the table is incomplete and different than usually. More specifically:

- they are missing the `Name` column that used to be in _third_ place,
- the table is sorted by weight, it used to be sorted by name,
- the age of the animals should show the age in years and not the birthdate
  - a composable for this already exists, made by the previous zookeeper

Please fix the two above problems and outline what was necessarry to do so.

// Your solution

1. Put the Name Column Back in the Right Spot
   The "Name" column had gone missing or was in the wrong place. It needed to be added back as the third column in the table so it matched the original layout.

2. Sort the Animals by Name using "localeCompare"
   The table was sorting animals by their weight, but it used to be sorted by their names. This was fixed by making sure the list of animals is sorted alphabetically by name before showing it.

3. Show Age Instead of Birthdate
   The table was showing each animal’s birthdate, but it’s more useful for the zookeepers to see how old the animals are. There was already a helper function (written by a previous zookeeper) that calculates age in years from a birthdate, so that was used as "useAge" to show the animal’s age instead.

### Task 6: UI Feature 1

The zookeepers want to be able to see all details of an animal. Please create such a view that allows them to do so, outline anything about your process while adding the view below. The zookeepers didn't have time for more information, sorry. They'll surely be glad to criticize the first version intensly though and will want to know why you went for the approach you chose.

// Your solution

In the animal table, we can now click on an animal’s name. When we do, a popup (called a modal) opens up, showing all the details we have about that animal.

- For this I have created file.
  Location: "components/AnimalDetail.vue"

- This includes: Name, Species, Gender, Age, Height, weight, Favourite fruit, required food.

Bonuse - We also added a little extra: at the bottom of the popup, you will see how much food all the animals need this month.

### Task 7: Logic Feature

The zookeepers want a new feature: Calculate the food required for the next calendar month. Basically, the zookeepers want to ease their job and buy a month worth of food in advance. In order to do so they want you to calculate and display the food all animals need for the next month.

To calculate the food an animal needs in kilograms in 1 day, the zookeepers use the following formula:

1. Take height + weight and divide it by 250
2. If the animal is:
   - older than 20 years, half the required food,
   - younger than 2 years, double the required food
3. Cherrys have less calories, so if the favourite fruit of the animal are cherries, add 28 kg
4. If the animal is male, add 20 %
5. If the animal is a fish: The required food is 0 kg

// Your solution

I have created Calculation file [ Location: "utils/foodCalculation.ts" ] here to perform the task and made necessary changes here in "components/TheAnimalTable.vue".

### Task 8: Plan New Feature

After the disastrous specification of the new UI feature in the previous task, the zooplanners now want to sit down with you to plan the next feature better before implementation begins. Together you come up with requirements that you write down from the user-perspective (the zookeepers):

- I want to plan when to feed which animal,
- Per animal I want to be able to plan a day + a fruit that I feed them
- There should be an overview of all upcoming feeding tasks that tells me:
  - the animal name,
  - the food fruit,
  - the required amount of food
- the required amount of food is calculated using the algorithm from the previous task
- Tasks should be grouped by day, so that I have something like a "todo" list for each day
  - so for exmaple a structure like:
    - 24.03.2012
      - Anni, Bananas, 20kg
      - Belfried, Cherries, 10kg
    - 27.03.2012
      - ...
    - ...

Please create a breakdown for this feature. You can focus on aspects like: What tasks do we need to cover, what should their order be, how will the UI/UX be designed, what questions arise from the potentially inconsistent or incomplete staff requirements?

Don't spend more thatn 15-30 minutes here - planning like this can quickly become quite complex and we want to prevent this challenge taking too much of your time!

// Your solution

1. A small form to add feeding task
   Which includes: Animal(using dropdown), the fruit, date(using date picker)
2. It will show by grouping each day
   - 24.03.2012 - Anni, Bananas, 20kg - Belfried, Cherries, 10kg
     - 27.03.2012
       - ...
3. Food amount is auto calculated, we already have a function from previous task.

questions arise:

1. Can animals be fed more than once per day?
2. Does the fruit have to match the animal’s favorite?
3. Can a feeding task be edited or deleted later?
4. Are weekends or holidays different in any way?

### Task 9: Finish the documentation

Revisit docs from step 3, see if you want to add anything. Also think about bonuses. Add a general comment about anything (inside the universe of the challenge or out of it) if you want to.

// Your solution
Done.
