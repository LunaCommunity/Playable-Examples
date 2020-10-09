# Playable Examples
The repository contains simple playable HTML5 demos designed to be a reference for Playground preparation.

## Repository structure and intented use
The folders within this repository contain ready-to-use HTML5 pages that mimic the structure of real-world playable ads. Feel free to clone the repository, zip the contents of any folder and upload to your Playground account to see it in action.

## basic/ folder
This folder contains the minimal Playground-compatible example that consists of a single button trigerring the transition to an app store. It does not react to any events, has no configuration and serves primarily as a reference skeleton playable.

## full/ folder
This folder contains a fully featured example that includes a few configuration fields, the code that changes the apperance of the playable based on these values, and all mandatory callbacks' subscriptions (sound and pause state)ю

## Implementation Details

### Required

1. Please make sure your html file is named "source.html"
2. Use the Luna API when you want to direct the user to the app store: `Luna.Unity.Playable.InstallFullGame()`
3. Please make sure all the startup functionality is performed in the `startGame()` function

### Optional

Subscribe to the following events if you wish to handle certain behaviours in the ad: 

       /**
         * Subscribing to luna:build event – it is going to be fired right after 'load' event of the window.
         */
        window.addEventListener( "luna:build", function() { 
            log( 'Playable is about to start' );
        } );

        /**
         * Subscribing to luna:unmute event – the playable can play sounds once it is fired.
         */
        window.addEventListener( "luna:unmute", function() { 
            log( 'Playable needs to be unmuted' );
        } );

        /**
         * Subscribing to luna:mute event – the playable must mute all the sounds once it is fired.
         */
        window.addEventListener( "luna:mute", function() { 
            log( 'Playable needs to be muted' );
        } );

        /**
         * Subscribing to luna:pause event – the playable must pause rendering and sound playaback.
         */
        window.addEventListener( 'luna:pause', function () {
            log( 'Playable needs to be paused' );
        } );

        /**
         * Subscribing to luna:pause event – the playable must resume rendering and sound playaback.
         */
        window.addEventListener( 'luna:resume', function () {
            log( 'Playable needs to be resumed' );
        } );

        // check if Luna is defined in global namespace
        if ( 'Luna' in window ) {
            // it is - nothing to do, the startGame() will be invoked when needed
            log( 'window.Luna is set - startGame() will be called automatically' );
        } else {
            // it is not - probably a development build, invoke startGame() manually
            startGame();
        }

