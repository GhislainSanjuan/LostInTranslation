# Lost in translation : How to break the language barrier in Appsheet
When you work with several teams across the globe, language barrier can be a problem. 

Let’s say, you have an Appsheet wiki with informations about safety procedures. 

But teams in other countries want to be able to display the content in their own language…

So how to go from this to this ?
<img src="https://user-images.githubusercontent.com/GhislainSanjuan/LostInTranslation/blob/main/docs/1.png" width="200" />
![1](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/1.png?raw=true)

### 2 solutions
1.Create a Google Chrome extension translating the data
- Needs strong coding skills
- Needs to be tested with different environments (with or without VPN,security features,...)
> A complex solution

2.Adapt your Appsheet application to translate content
- No coding skills needed except literally 3 line of Apps Script 
- Stay in the Appsheet environment
> A much more affordable solution


### Architecture
In order to get translations and stay in Appsheet, we need to store the translated content. To do so we can have the following architecture :
![2](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/2.png?raw=true)

### Translation workflows
We need to to first translated the containers/fields display name
![3](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/3.png?raw=true)

Now we’ve translated containers, we need to create a workflow to translate content by just clicking on a button
![4](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/4.png?raw=true)

Let’s focus now on the SAFETY CARDS table to understand how to display the translated content/containers 
![4](https://github.com/GhislainSanjuan/LostInTranslation/blob/main/docs/5.png?raw=true)


