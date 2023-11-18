```plantuml

@startuml

title onClickPostWordFromUndo()

participant "End User" as user

box "FE" #Lightblue
  participant "Component" as fe
  participant "Hook" as hook
  participant "IsLoading" as useState
  participant "Recoil" as recoil
box
box "API" #Lightgreen
  participant "API" as api
box


activate user
  user -> fe: Click undo button
  activate fe
    fe -> hook: usePostWordFromUndo()
    activate hook
      hook -> useState: setLoading(true)
      activate useState
        useState -> useState: Sets isLoading to true
        hook <- useState: Done
      deactivate useState
      hook -> recoil: getPromise(wordsFamily(undoingWordId))
      activate recoil
        hook <- recoil: Return word data
      deactivate recoil
      break if word data is undifined
       user <- hook: show nothing / failed to re-post word
       end break
      hook -> api: postWordApi(word)
      activate api
        hook <- api: return repost word
      deactivate api
      hook -> recoil: getPromise(wordIdsState)
      activate recoil
       hook -> recoil: wordIdsState
      hook <- recoil: wordIdsState
      break wordIds
       hook -> hook: id -> postedWord.id //if wordId === undoing wordId
      hook -> hook: id //上記条件が満たされない場合は、そのままの値を保持
       end break
       hook -> recoil: set(wordIdsState, wordIds)
       hook -> recoil: set(wordsFamily(postedWord.id), postedWord)
       hook -> recoil: set(semestersState, semesters.semesters)
      deactivate recoil
      hook -> fe: usePostWordFromUndo
      hook -> useState: setLoading(false)
      fe -> user: show wordcards
      activate useState
        useState -> useState: Sets isLoading to false
        hook <- useState: Done
      deactivate useState
      fe <- hook: Returns undefined
    deactivate hook
    user <- fe: Returns nothing
  deactivate fe
deactivate user
