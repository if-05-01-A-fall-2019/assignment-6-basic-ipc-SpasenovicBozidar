*Bozidar Spasenovic*
# Race Condition

**What is a race condition?**<br/>
A race condition is a situation that arises when a System attempts to run two or more Operations.

# Disabling Interrupts

**Why is it impossible to achieve Mutual Exclusion via disabling interrupts on a multi-core machine?**<br/>
Because process can run at the same time

**Why is it dangerous to give user process the power to disable interrupts?**<br/>
Because other process can take forever to end and than the PC can freeze.<br/> Maybe he disable a process that another process needs to finish.

# Peterson's Solution

**Play through the two scenarios of the handout of Peterson's solution. Document how it works.**<br/>
*Scenario 1:*<br/>

        1. Process 0 get in enter_Region
        2. sets intrested[0] = true
        3. sets loser = 0
        4. enter the critical critical region
        5. the first 3 steps with proces 1
        6. he has to wait until process 0 leave the region
        7. after process 0 leav the region he sets intrested[0] = false
        8. proces 1 enter critical critical region

*Scenario 2:*

        The indexes of intrested[] are true, so the proces 0 sets loser = 0 and the process 1 does the same thing.
        Our loser is now process 1 and that means that process 1 stucks in the while, until process 0 leave the critical region

**Play through the scenario which makes the strict alternation approach fail. Document how it fails.**

Suppose process 0 gets the time to go through the entire loop, and the scheduler gives process 1 the time to do just one step of the loop.
Process 0 goes through the loop and sets turn = 1.
Process 1 checks turn != 1, which is wrong. So it goes to critical_region ().
But now it's the turn of Process 0 to see if turn! = 0 what is true.
This is checked so often until process 1 gets time to enter the CR.
But then it's time to check something that we know can not change in the time of Process 0.
But process 0 is constantly checking this.

**What is the meaning of the variable loser in Peterson's solution? When does it have any effect?**

The loser is the proces that has to wait for the other one to leave the critical region. The variable prevents other processes from entering the critical region if there is already a process in the critical region.
