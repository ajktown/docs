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
			  authPrep -> api: onGetAuthPrep
				activate api
				  break if there is no auth prep
					  authPrep <- api: return null
					end break
				  authPrep <- api: return data
				deactivate api
        break if there is no auth prep or the user is not signed in
          hook <- authPrep: throw new Error('Not Signed In')
          hook <- hook: handleSignOutApp()
        end break
        hook <- authPrep: Return undefined
        hook <- hook: router.push(DEFAULT_MAIN_APP_PAGE)
      deactivate authPrep
      fe <- hook: Returns nothing
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user





