# MaximizeVertically
max_vert.txt is an AppleScript that should be added to Automator

##Instructions for installation:
1. Open *Authomator*. You can do this with Spotlight search by hitting CMD-Space and type 'Automator'
2. Click *New Document*
3. Select *Quick Action*
4. In the second column on the left-side, Double-Click *Run AppleScript*
5. Paste the contents from below into that template
6. In the File menu, choose *Save*.
7. Give it a name like *MaximizeVertically*
8. This will create a new service that you can trigger with a hotkey
9. Test it by clicking the Apple menu and choosing *Services* and then *MaximizeVertically*
10. That should give you a pop-up saying whatever app you are in wants access to control "System Events.app". Go ahead and allow it
11. You'll get 2 more pop-ups, The first one is asking you to open system settings and grant access but the 2nd pop-up is covering that. You'll need to dismiss the 2nd pop-up so you can respond to the first. In my case, I was doing this from Alacritty so I had to give Apacritty Accessibility access.
12. Create a hot-key
   1. Go to System Settings -> Keyboard -> Keyboard Shortcuts...
   2. Within that, choose *Services*
   3. Expand *General*. You should see *MaximizeVertically*.
   4. Assign a hotkey to that. I chose Shift-CMD-0


`
on run {input, parameters}
	
	-- Get the frontmost application
	tell application "System Events"
		set frontApp to first application process whose frontmost is true
		tell frontApp
			tell window 1
				-- Get current window bounds {x, y, width, height}
				set windowBounds to position & size
				set xPos to item 1 of windowBounds
				set yPos to item 2 of windowBounds
				set currentWidth to item 3 of windowBounds
				set currentHeight to item 4 of windowBounds
				
				-- Set new height (change this value as needed)
				set newHeight to 2500
				
				-- Keep the same x position and width, only change height
				set position to {xPos, 0}
				set size to {currentWidth, newHeight}
			end tell
		end tell
	end tell
	
	return input
end run
`
