# On App Booting Hook

<!-- TOC -->

- [Use Is App Booted Hook](#use-is-app-booted-hook)
  - [Overview](#overview)

<!-- /TOC -->

## Overview
This is a basic activity diagram for the useIsAppBootedHook.


```plantuml

@startuml

title useIsAppBootedHook()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook: useIsAppBooted" as hook
	participant "UseAuthPrepHook" as authPrep
	participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box

activate user
	user -> fe: open app
	activate fe
		fe -> hook: useIsAppBooted
		activate hook
			hook -> authPrep: onGetAuthPrep
			activate authPrep
				break if there is no auth prep or the user is not signed in
					hook <- authPrep: throw new Error('Not Singed In')
					fe <- hook: router.push(DEFAULT_MAIN_APP_PAGE)
				end break
				hook <- authPrep: handleSignOutApp()
			deactivate authPrep
			hook -> recoil: useEffect()
			activate recoil
				break if isBooted is true
			  	hook <- recoil: Returns onAppBooting()
				end break
			deactivate recoil
			fe <- hook: Returns nothing
		deactivate hook
	  user <- fe: Returns nothing
	deactivate fe
deactivate user





