# Andriod_final
App with navigation and api

Team : Ekta Saraf (21BCE5397)
       Aanchal Singh(21BCE5447)
       Amancharla Manuhya(21BCE5455)

## Getting Started

### Prerequisites

Before you begin, make sure you have the following installed on your machine:

- [Node.js](https://nodejs.org/) (v14 or later)
- [npm](https://www.npmjs.com/) (v6 or later)
- [Expo CLI](https://docs.expo.dev/get-started/installation/) (for running the React Native app)

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/your-username/diary-app.git
    cd diary-app
    ```

2. Install dependencies:

    ```bash
    npm install
    ```

### Running the App

Start the React Native app using Expo:

```bash
npm start

Procedure :
Android library for managing multiple stacks of fragments (e.g., Bottom Navigation , Navigation Drawer). This library does NOT include the UI for bottom tab bar layout. For that, I recommend either BottomBar (which is the library shown in the demo) or AHBottomNavigation. This library helps maintain order after pushing onto and popping from multiple stacks(tabs). It also helps with switching between desired tabs and clearing the stacks.

 Initialize using a builder and one of two methods
 Create a list of fragments and pass them in;
 Allow for dynamically creating the base class by implementing the NavListener in your class and overriding the getRootFragment method
 val fragments = listOf(
                RecentsFragment.newInstance(0),
                FavoritesFragment.newInstance(0),
                NearbyFragment.newInstance(0),
                FriendsFragment.newInstance(0),
                FoodFragment.newInstance(0),
                RecentsFragment.newInstance(0),
                FavoritesFragment.newInstance(0),
                NearbyFragment.newInstance(0),
                FriendsFragment.newInstance(0),
                FoodFragment.newInstance(0),
                RecentsFragment.newInstance(0),
                FavoritesFragment.newInstance(0))

fragNavController.rootFragments = fragments

Send in the supportFragment Manager, a list of base fragments, the container that you'll be using to display fragments. After that, you have four main functions that you can use In your activity, you'll also want to override your onSaveInstanceState like so

Tab switching is indexed to try to prevent you from sending in wrong indices. It also will throw an error if you try to switch to a tab you haven't defined a base fragment for.

Push a fragment
You can only push onto the currently selected index
pop a fragment
You can only pop from the currently selected index. This can throw an UnsupportedOperationException if trying to pop the root fragment

        fragNavController.popFragment();
Pop multiple fragments
You can pop multiple fragments at once, with the same rules as above applying. If the pop depth is deeper than possible, it will stop when it gets to the root fragment

       fragNavController.popFragments(3);
Replacing a fragment
You can only replace onto the currently selected index

        fragNavController.replaceFragment(Fragment fragment);
You can also clear the stack to bring you back to the base fragment
        fragNavController.clearStack();
You can also navigate your DialogFragments using
        showDialogFragment(dialogFragment);
        clearDialogFragment();
        getCurrentDialogFrag()
Transaction Options
All of the above transactions can also be done with defined transaction options. The FragNavTransactionOptions have a builder that can be used.

class FragNavTransactionOptions private constructor(builder: Builder) {
    val sharedElements: List<Pair<View, String>> = builder.sharedElements
    @FragNavController.Transit
    val transition = builder.transition
    @AnimRes
    val enterAnimation = builder.enterAnimation
    @AnimRes
    val exitAnimation = builder.exitAnimation
    @AnimRes
    val popEnterAnimation = builder.popEnterAnimation
    @AnimRes
    val popExitAnimation = builder.popExitAnimation
    @StyleRes
    val transitionStyle = builder.transitionStyle
    val breadCrumbTitle: String? = builder.breadCrumbTitle
    val breadCrumbShortTitle: String? = builder.breadCrumbShortTitle
    val allowStateLoss: Boolean = builder.allowStateLoss
Get informed of fragment transactions
Have your activity implement FragNavController.TransactionListener and you will have methods that inform you of tab switches or fragment transactions

A sample application is in the repo if you need to see how it works.

Fragment Transitions
Can be set using the transactionOptions

Restoring Fragment State
Fragments transitions in this library use attach()/detch() (http://daniel-codes.blogspot.com/2012/06/fragment-transactions-reference.html). This is a delibrate choice in order to maintain the fragment's lifecycle, as well as being optimal for memory. This means that fragments will go through their proper lifecycle https://developer.android.com/guide/components/fragments.html#Lifecycle . This lifecycle includes going through OnCreateView which means that if you want to maintain view states, that is outside the scope of this library, and is up to the indiviudal fragment. There are plenty of resources out there that will help you design your fragments in such a way that their view state can be restored https://inthecheesefactory.com/blog/fragment-state-saving-best-practices/en and there are libraries that can help restore other states https://github.com/frankiesardo/icepick
