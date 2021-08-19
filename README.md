# COMP1511-Assignment-2

# Castle Defense

Attention brave and noble engineers! Castle CSE is under attack by Enemies from Frankie the Fox&#39;s Lair. Queen Chicken, First of Her Name, Protector of the Realm, Lecturer in Charge for COMP1511, has commissioned you to build Her defenses and protect Her Castle.

In this assignment, you will be implementing Castle Defense, a program that simulates an imaginary Realm that is under attack. You will be creating Lands in the Realm as well as building Towers to defend a Castle.

The Enemies will spawn from their Lair and move towards the Castle through the Lands. As the Enemies move, they will be attacked by the towers, which both harms the Enemies and depletes the towers. If the Enemies reach the Castle, they will damage it.

Your program will be managing Enemy movement as they pass through the Lands. It will also be managing the use of Towers against the Enemies and any damage the Castle receives.

**Note:**  If this assignment appears daunting, fear not! The Queen&#39;s chosen human (Marc in lectures) will be demonstrating many of the techniques necessary to begin your tasks. Her loyal subjects (the Tutors) will also be teaching some of the techniques in detail in Labs. During Week 8, a great deal of the course will be dedicated to helping you get started with this assignment.

The Realm

The realm is a struct that contains all of the objects that will be used in this assignment. Those are: Lands, The Lair, The Castle, Towers and Enemies. Your job is to manage the Realm, and everything it contains.  ![](RackMultipart20210819-4-ja71cd_html_a80558adfd63a73.jpg)

The Realm struct has a pointer to the Castle, whence Queen Chicken and her Loyal subjects look down upon their kingdom. It also has a pointer to the lair, from which Frankie the Fox sends his feindish Enemies. Every location in the Realm lies on a linked list that starts at The Castle, and goes down to The Lair. Locations can have one of four types:

- _Castle_: The Castle, which is always the first node in the linked list. If the Enemies can reach The Castle, they will deal damage to it.
- _Land_: A place where Enemies can gather.
- _Tower_: A defense, built by you, to attack Enemies
- _Lair_: The place from which Enemies are sent by Frankie

Your code should ensure that at the start of the program, the Castle points to the Lair, and the Lair points to NULL. Your code should then ensure that the Castle is always connected (through other locations) to the Lair; and that the Lair points to NULL.

To ensure this is true, you will never be given a test case where you are asked to put a tower after the Lair. (More details on adding towers later)

As an additional restriction to make the assignment&#39;s rules simpler, there will never be two locations with the same name.

Enemies

In these dark times, the realm is under attack. Fiendish Enemies regularly appear at their Lair and make their way, one location at a time, towards The Castle.

![](RackMultipart20210819-4-ja71cd_html_4aaa8dd55bd8bdc3.jpg)

An Enemy is represented by a struct which records their name, their maximum health and their current health (as integers). These structs should also be set up so that the Enemies can be joined together in a linked list.

Enemies will always be at a location, which is represented by a linked list of Enemies at every location in The Realm. Linked lists of Enemies are always listed in alphabetical order.

An Enemy dies when it has zero or less health. It then is removed from the linked list that contained it and its memory is freed.

There will never be two enemies in the realm with the same name.

Towers

![](RackMultipart20210819-4-ja71cd_html_35cd07fb2c29b4d4.jpg)

As mentioned before, locations in the realm can be Towers. Towers are able to reduce the HP of any Enemy at their Location. They can only be used a fixed number of times. When they run out of uses, they convert back into lands.

Towers have two important properties:

- _Power_: How much an Enemy&#39;s HP is reduced when the Tower attacks. This is a whole number, greater than zero.
- _Uses_: A count of how many times a Tower can be used before it reverts to being a land. This is a whole number, greater than zero.

The Castle

At the start of the list is The Castle. Enemies that manage to reach The Castle will deal damage to it; and if they move beyond the castle they are removed from the realm.

The Castle starts off with STARTING\_CASTLE\_HP health. If an Enemy damages The Castle, it causes The Castle&#39;s health to decrease by that Enemy&#39;s remaining health.

**Note: ** Nothing special should happen when the castle goes below 0 HP. It can go negative if enough damage is dealt to it.

The Game

When the game starts, two locations are automatically created - the Castle and the Lair. You will then be given a list of locations on standard input, one per line. The order of the locations as standard input is the same order they will have starting from Castle and proceeding to Lair. These locations will be strings that do not contain any spaces, dashes or square brackets. When the list of locations is complete, an empty line will be input.

After this, a prompt will appear. You will type in commands to indicate changes to the state of the Realm. These commands will all start with a character as the command, then a space, then possibly some additional information about the command. There are three special commands, which are already implemented in the Starter Code provided. They consist of:

- ?: Print a list of all possible commands.
- q: Quit the program.
- /: Do nothing, this line is treated as a comment.

# Your Task: Implementation

Your task for this assignment is to write the functions that will manage the state of the Realm. All of these functions are contained inside the file realm.c. You will also have to write functions in test\_realm.c to check your code works.

Starter Code

[**Download the starter code (castle\_defense.zip) here** ](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/castle_defense.zip)or copy it to your CSE account using the following command:

**1511 setup-castle-defense**

The starter code consists of the following files:

[main.c](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/main.c) contains the main function for the assignment. It will scan the program&#39;s input, then call the functions you will write.  **You must not change this file.**

[realm.h](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/realm.h) contains the definitions of all the functions you will be writing. It also contains useful constants and type definitions.  **You must not change this file.**

[realm.c](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/realm.c) contains empty functions which you will need to implement. It already contains some functions. It is _strongly recommended_ that you use these.  **This file is where you will write your own code.**

[test\_realm.h](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/test_realm.h) contains the prototypes of the testing functions in test\_realm.c.  **You must not change this file**

[test\_realm.c](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/test_realm.c) contains an alternative main function as well as template code that you will modify to make your own tests.  **This file is where you will write your own test cases.**

[capture.h](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/capture.h) contains the definition of a function that allows you to capture the output of your own code, to use in testing. It can only be used in test\_realm.c, and will not be available in realm.c.  **You must not change this file.**

[capture.c](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/capture.c) contains the implementation of functions that allow you to capture the output of your own code, to use in testing.  **You must not change this file.**

To run your code interactively, you should use the command:

**dcc -o castle\_defense realm.c main.c**

**./castle\_defense**

To run your tests (written in test\_realm.c), you should use the command:

**dcc -o test\_castle realm.c test\_realm.c capture.c**

**./test\_castle**

Allowed C Features

In this assignment, there are two restrictions on C Features:

- You must follow the rules explained in [the Style Guide](https://cgi.cse.unsw.edu.au/~cs1511/19T2/resources/style_guide.html).
- You may not use the function fnmatch, or import fnmatch.h.

It is recommended to only use features that have been taught in COMP1511. Course work in Week 8 will have a particular focus on assistance for this assignment and you will not need any of the subject material from Weeks 9 or 10.

If you choose to disregard this advice, you  **must**  still follow the Style Guide. You also may be unable to get help from course staff if you use features not taught in COMP1511.

Input Commands

Input to your program will be via standard input (similar to typing into a terminal). You  **do not**  need to read this input yourself. Your functions in realm.c will be called by main.c with the input already scanned in.

Your code should not print or scan from the terminal (standard input or output). Do not use or add any printf or scanf in realm.c unless it&#39;s temporary and for debugging purposes. All printing and scanning has already been implemented for you in the starter code.

You can assume that input will be handled for you, and that you will never be given an invalid argument to one of your functions (except as described below).

Details of how this input will relate to the functions you call are given below:

# Stage One

Stage one involves adding new locations to the realm, as well as being able to print out the game state.

Adding to the Realm

In realm.c you have been given two function stubs (a stub is an unimplemented function):

static Location new\_location(char \*name) {

return NULL;

}

int add\_location(Realm realm, char \*name) {

return 42;

}

These two functions should be implemented as described below.

new\_location should use malloc to allocate memory for a new Location node. It should then set up it&#39;s name (and any other fields you decide you need throughout the assignment).

- Note that the word &quot;static&quot; on this function will make it accessible within this file, but not elsewhere. We often use static on helper functions that are not part of the header file and aren&#39;t used by any other parts of the program. Static will not significantly change how you will use this function.
- The new\_realm function (already implemented in the starter code) uses the new\_location function. The new\_realm function does not need changing for this stage, but you may want to add code to it at a later stage.

add\_location will be given a Realm and a Location name. It will then insert a new location node directly before the Lair in the linked list of locations. It returns the number of locations in the linked list.

These functions will never receive invalid inputs.  ![](RackMultipart20210819-4-ja71cd_html_a6905cdb59da02de.jpg)

Printing Out the Realm

In realm.c you have been given the function stub:

void print\_realm(Realm realm) {

}

as well as four fully implemented functions:

void print\_tower(char \*name, int power, int uses, Effect effect);

void print\_land(char \*name);

void print\_castle(char \*name, int defense);

void print\_enemy(char \*name, int cur\_hp, int max\_hp);

print\_realm will be given a realm, and will print out information about that realm. You should use the functions given in the starter code to print it out, instead of calling printf yourself.

Specifically, print\_realm will list locations in order from The Castle to The Lair. If there are any enemies at a location, it will list them in order before listing the next location.

**Note:**  the castle starts off with STARTING\_CASTLE\_HP, so in the early stages, you will need to pass defense as STARTING\_CASTLE\_HP. You will not need the print\_tower and print\_enemy functions until Stage 2.

[Show Example: Stage 1 Example](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#s1a)

**Run the tests for this stage with:**

**1511 autotest-stage 01 ass2\_castle\_defense**

Please note, the files you test  **must**  be named correctly, or this test will not work properly.

**To pass all the tests for this stage, you will need to add tests in **** test\_realm.c** See [Writing your own automated tests](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#test_realm) for more info.

# Stage Two

Stage Two has two new commands. They involve adding enemies to a location, and adding Towers to protect the realm.

Add Enemies

When running the program, you can use the following command to add a new enemy:

e location\_name name HP

// for instance

e Lair EnemyName 4

Which means &quot;Create a new enemy, at the location location\_name, called name, with maximum HP hp.

You have been given the function stub, which will be called by main.c when the above command has been given:

int new\_enemy(Realm realm, char \*location\_name, char \*name, int hp) {

}

Your job is to implement this function, such that the code does the following:

Given a realm, the name of a Location in the realm, and some stats about a new enemy, you should (_in this order_):

- Find the Location called location\_name. If one does not exist, return ERROR\_NO\_LOCATION
- Ensure that the stats you have been given for HP are not below 1. If they are, return ERROR\_INVALID\_STAT.
- Place a new enemy, with the given stats, directly after the last enemy at the location you found above.
- Return SUCCESS to indicate success.

You are guaranteed that you will only receive enemies in sorted order, and will never receive the same enemy name twice. You do not need to check this. This means that for any list of enemies, strcmp(enemy-\&gt;name, enemy-\&gt;next-\&gt;name) will be _strictly less than zero_. This guarantee will only be relevant for Stage 4.

New Towers

When running the program, you can use the following command to add a new tower:

t prev\_name name power uses

// for instance

t Castle NewTower 2 2

Which means &quot;Create a new tower, directly below the Location prev\_name , called name, that causes power damage to each enemy at it, and that can be used uses times&quot;.

You have been given the function stub, which will be called by main.c:

int new\_tower(Realm realm, char \*prev\_name, char \*name, int power, int uses){

}

Your job is to implement this function, such that the code does the following:

Given a realm, the name of a Location in the realm, and some stats about a new tower, you should:

- Find the Location called prev\_name. If one does not exist, return ERROR\_NO\_LOCATION
- Ensure that the stats you have been given for power and uses are not below 1. If they are, return ERROR\_INVALID\_STAT.
- Place a new tower, with the given stats, directly after the location which you found above. This tower is inserted into the linked list, which adds an element and does not replace the Location prev\_name.
- Return SUCCESS to indicate success.

![](RackMultipart20210819-4-ja71cd_html_230912640f8f906e.jpg)

[Show Example: Stage 2 - Printing Example With Towers/Enemies](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#s2a)

**Run the tests for this stage with:**

**1511 autotest-stage 02 ass2\_castle\_defense**

Please note, the files you test  **must**  be named correctly, or this test will not work properly.

**To pass all the tests for this stage, you will need to add tests in **** test\_realm.c** See [Writing your own automated tests](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#test_realm) for more info.

# Stage Three

Stage Three involves destroying the realm, advancing enemies through the realm, and applying damage to them.

Freeing Memory and Destroying the Realm

When you quit the program (using the special command q), the following stub function will be called to free your list.

void destroy\_realm(Realm realm);

calling this function should free:

- Each Enemy
- Each Location
- The Realm struct
- Any other memory you have allocated using malloc

Advancing Enemies

When running the program, you can use the following command to move all enemies along.

n

This is called a &quot;tick&quot; in game design (as in, the &quot;tick&quot; of a clock). You have also been given the following function stub:

int advance\_enemies(Realm realm) {

}

advance\_enemies will go through the realm, moving each enemy from their current Location to the Location above in the linked list. Should any enemies go above the castle, they should be removed from the realm, and destroyed. You should return the number of enemies removed this way at the end of the function. The Lair should be empty of enemies after this, all of them having moved to the next Location in the list.  ![](RackMultipart20210819-4-ja71cd_html_49483bbfbd8b7447.jpg)

Damage

When running the program, you can use the following command to deal damage to Enemies and The Castle. It will also use up &quot;uses&quot; from any Towers that deal damage to enemies.

You can deal damage using the following command:

d

This will call the following function stub:

int apply\_damage(Realm realm) {

}

Go through each Location in the realm, and do the following if the Location is a Tower:

- Go through each Enemy at that Tower, and reduce it&#39;s HP by the Tower&#39;s power. If an enemy&#39;s HP is equal to or less than zero, remove it from the list of Enemies at that location
- Reduce that Tower&#39;s number of uses left by 1, if it did damage to an enemy.
- If that Tower now has no uses remaining, convert it into a Land. It should no longer have any effect on enemies that pass through it.

apply\_damage should also cause the Castle&#39;s defense to decrease, by the sum of the HP of each enemy currently at the Castle. For instance, if the Castle had an enemy with 3 HP, and one with 5 HP, the Castle&#39;s defense would decrease by 8.

apply\_damage returns the number of enemies damaged this way.

Before Applying Damage

![](RackMultipart20210819-4-ja71cd_html_1b94a8569354d529.jpg)

After Applying Damage

![](RackMultipart20210819-4-ja71cd_html_e7e23409fde2c4cf.jpg)

**Run the tests for this stage with:**

**1511 autotest-stage 03 ass2\_castle\_defense**

Please note, the files you test  **must**  be named correctly, or this test will not work properly.

**To pass all the tests for this stage, you will need to add tests in **** test\_realm.c** See [Writing your own automated tests](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#test_realm) for more info.

# Stage Four

Stage Four involves applying buffs (&quot;changes in stats&quot;) to different parts of the realm. It also uses the concept of a &quot;search&quot;, which is described below:

Searching

This has changed since the spec was released.

In the initial version, we asked for an &quot;exact match&quot;, when the sample solution and autotests implemented a &quot;prefix match&quot;. We have updated the specification to describe an prefix match; however, we will not write any tests during Stage 4 that confirm you wrote a prefix match rather than an exact match. In Stage 5, where there is already an autotest that relies on prefix matching, we will assume you have written a prefix match.

Stage Four and Five rely on the concept of a search, described by a search\_term. The simplest case is just a word, which should try find an _prefix_ match. A prefix match is one where the word _starts with_ the search term. For instance, searching for &quot;hi&quot; in the array {&quot;hiya&quot;, &quot;JBhi-fi&quot;, &quot;JBHi-Fi&quot;, &quot;hi&quot;, &quot;HI&quot;, &quot;phi&quot;} would find &quot;hiya&quot; and &quot;hi&quot;.

There is a special syntax we can use in a search, however, called a &quot;character class&quot;. This lets you say &quot;Any of these characters&quot;. A character class is wrapped in square brackets, like this: [abc]. That character class means &quot;either a or b or c&quot;. Note that a character class takes the place of a single character, so h[abc]k would match &quot;hak&quot; or &quot;hck&quot; but not &quot;hack&quot;.

There is also a shorthand in character classes for a group of characters: [a-m] means &quot;match any character with an ascii value equal to or above &#39;a&#39;, and less than or equal to &#39;m&#39;&quot;. In other words, it would match lowercase letters before &#39;n&#39;.

You can mix and match these styles, so [0-9abD-F] would mean &quot;match a character between &#39;0&#39; and &#39;9&#39;, or &#39;a&#39;, or &#39;b&#39;, or a character between &#39;D&#39; and &#39;F&#39;.

You may assume that search terms always have matching &#39;[&#39; and &#39;]&#39; characters, and that &#39;-&#39; will never be the first or last character in a character-class. The character classes [] and (for example) [f-d] are both valid, but would never match anything.

You may also assume that locations and enemies will never have &#39;[&#39;, &#39;-&#39; or &#39;]&#39; in their name. You do not need to check this. Until July 23, an autotest had contained an enemy with a &#39;-&#39;, but this autotest has been altered to replace the &#39;-&#39; with a &#39;\_&#39;.

Buffs

You may use the following command to apply a buff. It is explained below

b search\_term buff\_type buff\_amount

Using this command will call the following function stub:

int apply\_buff(Realm realm, char \*search\_term, Buff buff, int amount) {

}

This means to apply the buff described by buff\_type to everything matching search\_term

There are three separate Buffs, each of which behaves differently.

| Name | Character (part of the command) | Buff Hash Define (defined in realm.h) | Description |
| --- | --- | --- | --- |
| Buff Enemy HP | h | BUFF\_ENEMY\_HP | Find all Enemies in the Realm with a name that matches the search described by search\_name. You should then increase each of their HP by the specified amount. Return the number of enemies you found this way.This amount can be negative. If a negative amount would cause an Enemy to drop to zero or less HP, it dies (as if had been killed after the apply\_damage function).An Enemy can have more current HP than its maximum HP. This buff should not change the maximum HP of an Enemy. |
| --- | --- | --- | --- |
| Buff Tower Power | p | BUFF\_TOWER\_POWER | Find all towers in the Realm with a name that matches the search described by search\_name. You should then increase each of their power by the specified amount. Return the number of towers you found this way.This amount can be negative. If a negative amount would cause an tower to drop below 1 power, it should be converted to a land, (as if had run out of uses after the apply\_damage function). |
| Buff Tower Uses | u | BUFF\_TOWER\_USES | Find all towers in the Realm with a name that matches the search described by search\_name. You should then increase each of their uses by the specified amount. Return the number of towers you found this way.This amount can be negative. If a negative amount would cause an tower to drop below 1 use remaining, it should be converted to a land, (as if had run out of uses after the apply\_damage function). |

**Run the tests for this stage with:**

**1511 autotest-stage 04 ass2\_castle\_defense**

Please note, the files you test  **must**  be named correctly, or this test will not work properly.

**To pass all the tests for this stage, you will need to add tests in **** test\_realm.c** See [Writing your own automated tests](https://cgi.cse.unsw.edu.au/~cs1511/20T2/assignments/ass2/index.html#test_realm) for more info.

# Stage Five

**This stage has very few tests!**  This stage has 2 tests, one for each effect. They do not necessarily cover every edge case. You should test it with other inputs, and compare your solution against the reference solution.

Effects

You may use the following command to change a tower&#39;s effect. It is explained below.

f search\_term effect\_type

Using this command will call the following function stub:

int apply\_effect(Realm realm, char \*search\_term, Effect effect) {

}

This means to apply the effect described by effect\_type to every tower matching search\_term

This function should return the number of towers that match the search\_term

There are two effects you can apply, as well as the EFFECT\_NONE which removes any special effect from a tower.

All towers start with EFFECT\_NONE when they are created. Enemies move from that Tower to the next as normal.

When a tower&#39;s effect becomes something other than EFFECT\_NONE, enemies move from that Tower in a different way. The specifics depend on which effect is applied to a tower, and is described below

Note that these Effects only change the way Enemies move. A Tower that has an effect will still deal damage and lose uses when applying damage, regardless of any effect they have. A Tower that is reduced to 0 uses and reverts to a Land will lose any Effects it has.

| Name | Character (part of the command) | Effect Hash Define (defined in realm.h) | Description |
| --- | --- | --- | --- |
| None | n | EFFECT\_NONE | All Towers start off with this effect. Enemies at this Tower move to the next Location normally when all enemies are moved. |
| --- | --- | --- | --- |
| Ice Tower | i | EFFECT\_ICE | If an Enemy would move from the Tower with this effect (&quot;the current tower&quot;) to the next Location, and that enemy has HP less than the current tower&#39;s power, it stays at the current Tower. Enemies at other locations (which don&#39;t have effects) move normally.Enemies at every Location must be sorted alphabetically. You should ensure that this movement preserves the alphabetical ordering of enemies. |
| Portal Tower | p | EFFECT\_PORTAL | After all enemies have moved, if there are enemies at portal towers, they should all be moved back to the Lair. This effect is removed from a tower after it has finished moving enemies.Enemies at every Location must be sorted alphabetically. You should ensure that this movement preserves the alphabetical ordering of Enemies. |

Ice Effect Diagram

![](RackMultipart20210819-4-ja71cd_html_9d21f4606c7cca5e.jpg)  ![](RackMultipart20210819-4-ja71cd_html_c0311713961417c0.jpg)

Portal Effect Diagram

![](RackMultipart20210819-4-ja71cd_html_33ac0a6f6e8cc625.jpg)  ![](RackMultipart20210819-4-ja71cd_html_9a27ea7deb6c8df0.jpg)

**Run the tests for this stage with:**

**1511 autotest-stage 05 ass2\_castle\_defense**

Please note, the files you test  **must**  be named correctly, or this test will not work properly.

# Testing

It is important to test your program thoroughly to make sure it can manage different situations.

Writing your own Automated Tests

As you implement functions in  **realm.c** , you will encounter autotests in that ask you to implement [test\_realm.c](https://cgi.cse.unsw.edu.au/~cs1511/20T2/activities/castle_defense/test_realm.c).

test\_realm.c is a file that contains a main function that is not the same as the interactive program in main.c. Instead, it runs a series of automatic tests on the functionality provided by realm.h and realm.c. You should not change this main function.

Your main function will call other functions that look like this:

void test\_add\_location(void) {

printf(&quot;Test whether this add\_location follows the spec: &quot;);

// Test 1: Does add\_location&#39;s return value count the Castle &amp; Lair?

Realm test\_realm = new\_realm();

int num\_locations = add\_location(test\_realm, &quot;Location&quot;);

if (num\_locations != 3) {

printf(DOES\_NOT\_FOLLOW\_SPEC);

return;

}

// Test 2: Does add\_location return the correct amount for lots of locations?

// TODO: Change Here

// Test 3: Add your own test, and explain it below:

// ........

// TODO: Change Here

printf(FOLLOWS\_SPEC);

}

Your job is to fill in the spaces where it says &quot;Change Here&quot; with a series of C statements that check whether the functions in realm.c work.

As you can see in Test 1, some of these functions have already been partially implemented to show you what you should do

Some functions will ask you to specifically test something (in this case, to make sure add\_location returns the correct amount if you call it many times).

Some functions will ask you to decide on your own test. You should describe what you are testing, and then write a test for that thing.

Note that you can  **only**  test functions by checking their return values, and their output to the terminal. You cannot access the fields of a struct, nor can you redefine the structs from realm.c in test\_realm.c. Doing so may cause you to lose marks.

You can test your tests yourself, by compiling it against your realm.c.

This is what you will see when you compile the starter code/tests.

**dcc -o test\_castle test\_realm.c realm.c capture.c**

**./test\_castle**

================== Castle Defense Tests ==================

Test whether this add\_location follows the spec: Does Not Follow Spec.

Test whether this print\_realm follows the spec: Does Not Follow Spec.

Test whether this new\_enemy follows the spec: Follows Spec.

Test whether this new\_tower follows the spec: Follows Spec.

Test whether this apply\_damage follows the spec: Follows Spec.

**New (as of 22nd July): **You are now able to compile your test code against our broken code. To do so, run 1511 build-test-castle test\_realm.c -o test\_realm.

You can then choose one of the &quot;defects&quot; that our test code supports, and the test solution will misbehave.

**1511 build-test-castle test\_realm.c -o test\_realm**

**./test\_realm**

================== Castle Defense Tests ==================

To use this test program, you should use:

./test\_realm DEFECT

Where DEFECT is one of:

- MANY\_LOCATIONS

- WRONG\_HP

- NO\_LAIR\_ENEMY

- TOWER\_AFTER\_TOWER

- DAMAGE\_NO\_DESTROY

- NONE

- NONE

**./test\_realm DAMAGE\_NO\_DESTROY**

================== Castle Defense Tests ==================

Test whether this add\_location follows the spec: Follows Spec.

Test whether this print\_realm follows the spec: Follows Spec.

Test whether this new\_enemy follows the spec: Follows Spec.

Test whether this new\_tower follows the spec: Follows Spec.

Test whether this apply\_damage follows the spec: Does Not Follow Spec.

Test whether this apply\_buff follows the spec: Follows Spec.

Capture

This term, we have given you two extra files -- capture.c and capture.h. These files define the CAPTURE macro. Macros are not covered in this course and as a result, you do not need to understand these files.

You can use them to capture what a function prints and put it into a string. This is useful if you combine it with the print\_realm function, since you can then test the realm is as you expect.

The header of capture.h describes how to use it.

// This file contains the `CAPTURE()` macro. To use this macro,

// you should define a large, empty string. Lets say your string is:

// char str[MAX\_LENGTH];

// Then you can do the following:

// CAPTURE(my\_function(), str, MAX\_LENGTH)

// Which will put the output of `my_function()` into str.

Autotests

As usual autotest is available with some simple tests - but your own tests in  **test\_realm**  may be more useful at pinpointing exactly which functions are and aren&#39;t working.

**1511 autotest castle\_defense**

If you wish to use autotest to view only a specific stage of the assignment, you can use autotest-stage. The following example shows how to autotest stage 1 but you can replace the stage number with any stage you would like to test.

**1511 autotest-stage 01 castle\_defense**

Reference Implementation

If you have questions about what behaviour your program should exhibit, we have provided a sample solution for you to use.

**1511 castle\_defense**

# Frequently Asked Questions

How many tests do I need to complete to get full marks?

You only need to complete the tests marked with &quot;TODO&quot;; except the extra\_tests which are optional. For each function, this means you will need to write two tests (note that this desn&#39;t include tests we have provided you). You do not need to write tests for stage five, though we encourage you to do so for your own learning and enjoyment!

What should towers print out as their effect in Stages 2 - 4?

By default, towers have the effect EFFECT\_NONE. This is a hash-define, and in stages two through four, you can just pass this hash define as the effect.

How do the autotests for test\_realm.c work?

Your test\_realm.c is designed to test whether the realm.c it is compiled with works properly. The autotests will compile your test\_realm.c with a  **deliberately incorrect**  realm.c. This means that we expect your test\_realm.c to say that one of given functions &quot;Does Not Follow Spec.&quot;.

For instance, in the 01\_test\_add\_location test, we expect that your test\_add\_location function will print &quot;Does Not Follow Spec&quot;, but all your other test functions should print &quot;Follows Spec.&quot;.

I don&#39;t know what tests to write in test\_realm.c!

We suggest the easiest way to get started on testing is to copy the given tests, and modify them slightly. The test functions for stages 1, 2 and 3 give you some specific properties to test for, so try to write a test for them. This is usually as simple as calling a few functions from realm.h then either checking their return values, or using the CAPTURE macro and then string\_contains. Once you&#39;ve got a hang of it, come up with your own tests too! You might want to consider what happens if you have multiple realms, or if there are invalid inputs you are supposed to check for. You can go as crazy as you like, but we recommend you try to test errors that you think somebody could actually make -- imagine your tests were being run against someone else&#39;s code: would they catch something?

Why can&#39;t I access structs from realm.c inside of test\_realm.c?

The way C works is if the struct definition is not present in the current .c file then the code there is not able to access the members of that struct. You can create a pointer variable which points to that struct, but you will not be able to access it&#39;s members with -\&gt;. This is a good thing, and is intended.

This design feature is because it allows us to implement Abstract Data-Types (ADTs). The objective of using ADTs is so that the code of one file can not access the &quot;inner workings&quot; of a variable that it uses, but is restricted to calling functions from a .h file with that variable. This may sound counter productive at first, why would you want to limit access to a variable? Actually there are several advantages:

1. **Access Control** : This is a useful concept when you have multiple programmers working together. It allows you to police the things that happens to your Realm. If you are the creator of the data type (the realm) you can prevent other people (who may not know what their doing) from changing pointers (perhaps accidentally) in your data structure and in general ruining things.
2. **Abstraction** : It presents a simple interface (defined in the .h file) to use the code of your Realm. If you are the user of the data type someone else has created, it is really helpful to be presented with a simpler interface which hides the details of the underlying data structures, so they don&#39;t have to learn as many things to be able to use your data type.
3. **Decoupling** : All test\_realm.c files will conform to a common interface. Perhaps the way the other students in this course organised the members in their structs might be different to the way you&#39;re doing it. Tests which don&#39;t directly interact with the realm&#39;s members are interchangeable in this sense, one student&#39;s tests could be paired up with another student&#39;s realm and there wouldn&#39;t be any compatibility issues there.

So, to fix your error, try to design tests which don&#39;t stab -\&gt; into the realm, just call the functions in realm.h and check their outputs are correct/they did the correct things.

(Answer adapted from a forum post by Dean Wunder)

Can I define structs from realm.c in test\_realm.c?

Unfortunately no, See above.

Why do I keep getting the Incomplete definition of type ... error?

See above.

How does leakchecking work in this assignment?

Partway through the assignment, we realised some student had autotests that weren&#39;t using leakcheck. Because it would be unfair to enable leakcheck and potentially cause students to have to go back, we have added extra autotests to check for leaks. You do not need to pass these autotests, but you do need to make some attempt at freeing memory in stages 3-5. If you just leave the freeing functions blank, or make no effort at freeing memory, you will not have met the specification, and will therefore not gain full marks. We strongly encourage you to pass these leakchecking autotests, but if you&#39;ve already completed the assignment, and you use free (but aren&#39;t sure you catch every memory leak) we won&#39;t penalize you for having started early.

I&#39;m trying to test add\_location, how can I use a while loop?

First of all - using a while loop here is an excellent idea! Unfortunately, we had to require in this assignment that location names be unique. So, how can you make location names that are unique?! Well there are two options:

- You&#39;ve already been taught how to modify a character in an array. Consider how you might use this knowledge to add locations in order, like: &quot;LocationA&quot;, &quot;LocationB&quot;, &quot;LocationC&quot;, etc.
- Alternatively, there&#39;s another function we have not taught you in this course: sprintf (string printf). This function works just like printf, except you give it an extra first argument -- a string. If i had value 3, sprintf(str, &quot;Location\_%d&quot;, i); would be the same as strcpy(str, &quot;Location\_3&quot;);.

Can I use external libraries we haven&#39;t been taught?

As a general rule, using libraries we haven&#39;t taught you will make for more work. We have explicitly banned fnmatch.h, but apart from that you could choose to use untaught libraries. Doing so will likely make your program harder to read, and may cause you many bugs.

# Assessment

Attribution of Work

This is an individual assignment. The work you submit must be your own work and only your work apart from exceptions below. Joint work is not permitted.

You may use small amounts (\&lt; 10 lines) of general purpose code (not specific to the assignment) obtained from site such as Stack Overflow or other publically available resources. You should attribute clearly the source of this code in a comment with it.

You are not permitted to request help with the assignment apart from in the course forum, help sessions or from course lecturers or tutors.

Do not provide or show your assignment work to any other person (including by posting it on the forum) apart from the teaching staff of COMP1511.

The work you submit must otherwise be entirely your own work. Submission of work partially or completely derived from any other person or jointly written with any other person is not permitted. The penalties for such an offence may include negative marks, automatic failure of the course and possibly other academic discipline. Assignment submissions will be examined both automatically and manually for such submissions.

Relevant scholarship authorities will be informed if students holding scholarships are involved in an incident of plagiarism or other misconduct. If you knowingly provide or show your assignment work to another person for any reason, and work derived from it is submitted you may be penalized, even if the work was submitted without your knowledge or consent. This may apply even if your work is submitted by a third party unknown to you.

Note, you will not be penalized if your work is taken without your consent or knowledge.

Submission of Work

**You are required to test and/or submit intermediate versions of your assignment. ** Every time you work on the assignment and make some progress you should copy your work to your CSE account and submit it using the give command, or autotest it using 1511 autotest

It is fine if intermediate versions do not compile or otherwise fail submission tests.

Only the final submitted version of your assignment will be marked.  **You must **** give **** when you have completed your assignment.**

If you would like to retrieve your old work, you can go to: [View Autotests/Submissions/Marking](https://cgi.cse.unsw.edu.au/~cs1511/20T2/student/) and click the yellow bubble next to ass2\_castle\_defense. This will show you a timeline of all the code you have submitted recently.

You submit your work like this:

**give cs1511 ass2\_castle\_defense realm.c test\_realm.c**

The only files you can modify are realm.c and test\_realm.c.  **It is not possible to add new files, or modify the other files we have given you**. If you believe you need to modify those files, you have misunderstood the specification. You should not modify your copies of those files in any way.
