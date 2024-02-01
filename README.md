# Lost in translation : How to break the language barrier in Appsheet

----
First of all 
- if you want to copy the application  : [Lost in translation](https://www.appsheet.com//templates/How-to-break-the-language-barrier-in-Appsheet?appGuidString=b1a21096-36d5-44c1-9350-640b34b95a28).
- If you want the explanation in Google Slides : [Slides Lost in translation](https://docs.google.com/presentation/d/1fBpucLWDtZVLkxB4z7XZk9h5-3jAmRlEvEZ-TgAYWF8/edit#slide=id.g2aadba26b00_0_32).


The context
----

When you work with several teams across the globe, language barrier can be a problem. 

Let’s say, you have an Appsheet wiki with informations about safety procedures. 

But teams in other countries want to be able to display the content in their own language…


|   ||
|------|---|
| So how to go from this to this ? |![1](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/1.png)|


## 2 solutions
1.Create a Google Chrome extension translating the data
- Needs strong coding skills
- Needs to be tested with different environments (with or without VPN,security features,...)
> A complex solution

2.Adapt your Appsheet application to translate content
- No coding skills needed except literally 3 line of Apps Script 
- Stay in the Appsheet environment
> A much more affordable solution


## Architecture
|   ||
|------|---|
| In order to get translations and stay in Appsheet, we need to store the translated content. To do so we can have the following architecture : |![2](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/2.png?raw=true)|




## Translation workflows
|   ||
|------|---|
|We need to to first translated the containers/fields display name | ![3](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/3.png?raw=true) |
|Now we’ve translated containers, we need to create a workflow to translate content by just clicking on a button|![4](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/4.png?raw=true)|
|Let’s focus now on the SAFETY CARDS table to understand how to display the translated content/containers |![4](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/4.png?raw=true)|

## Formulas
2 formulas are used : 
- for the virtual column itself 
```sql
if(
 isnotblank(
  any(
   select(TRANSLATIONS[Translation],
          and(
          USERSETTINGS('Language')=[Language],
          [external_id]=[_THISROW].[ID],
          [Field]="Title")
         )
     )
    ),
 any(
   select(TRANSLATIONS[Translation],
          and(
          USERSETTINGS('Language')=[Language],
          [Field]="Title")
         )
     ),
 "Title"
)
```
- for the display name or the virtual and database columns 
```sql
if(
 isnotblank(
  any(
   select(TRANSLATIONS[Translation],
          and(
          USERSETTINGS('Language')=[Language],
          [external_id]=[_THISROW].[ID],
          [Field]="Title")
         )
     )
    ),
 any(
   select(TRANSLATIONS[Translation],
          and(
          USERSETTINGS('Language')=[Language],
          [Field]="Title")
         )
     ),
 "Title"
)
```

Another formula is used in the action to get the SAFERTY CARD entry to translate. This formula needs to retrieve manually the field mapping because the LOOKUP formula does not allow dynamics return column
```sql
switch([Field],
  "Title",LOOKUP(maxrow("SAFETY_CARDS","Last modified"),"SAFETY_CARDS","ID","db_title"),
  "Description",LOOKUP(maxrow("SAFETY_CARDS","Last modified"),"SAFETY_CARDS","ID","db_description"),
  "KeyWords",LOOKUP(maxrow("SAFETY_CARDS","Last modified"),"SAFETY_CARDS","ID","db_keywords"),
  ""
)
```


Finally the Appsheet bot uses a little script from Apps Script to translate content and 
```javascript
function translateData(field,language) {
  return LanguageApp.translate(field, "", language)
}
```
## Views
Finally adjust the views to display the right content
|Type view : Details, Table,... (<> Form)| Type view : Form|
|---|---|
|Use the mirror virtual columns because they are the one with the translated content|Use the database columns because you need those to create data|
| `Title` `Description` `KeyWords` |`db_title` `db_description` `db_keywords`|

## How the application works for the user ? 

|   ||
|------|---|
|The user selects a language through USER SETTINGS table| ![6](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/6.png?raw=true) |
|The user selects a Safety card :  if there is already a translation, the content and container is displayed with its translation ; if not the use can hit the button translation. After a bit of time the content will appear translated | ![7](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/7.png?raw=true) |


## Application behaviour you can change

In the template application, some behaviours have been defined in a certain way, but you can change them : 
- When a safety card is update, all the previous translation are deleted to be generated again by users
- When a safety card is created, the translations could be created automatically
- When a language is added, the fields display name translations are added




