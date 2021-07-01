```
mutation movies_dramas {

 jaws: insertmovies_by_genre(
    value: { 
      genre:"Thriller", 
      year:2018,
      title:"Jaws",
      synopsis:"A movie about an angry Shark.",
      duration:112,
      thumbnail:"https://i.imgur.com/yinQyyT.mp4"}) {
    value{title}
  }

}
```
