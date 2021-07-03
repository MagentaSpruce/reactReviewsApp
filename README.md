# reactReviewsApp
This React project cycles through a list of reviews and includes a random button picker as well.

Constructing this app helped me to better learn and practice the following:
1) Using react-icons library
2) useState()

A brief overview of the pertinent React code is given below.

First the App() function return statement is constructed and the <Review /> component inserted.
```React
function App() {
  return (
    <main>
      <section className="container">
        <div className="title">
          <h2>our reviews</h2>
          <div className="underline"></div>
        </div>
        <Review />
      </section>
    </main>
  );
}
```


Next the functionality for the Review component was built out using the imported people data. The people data array has state watching it and the people array is deconstructed for use in the return statement.
```React
const Review = () => {
  const [index, setIndex] = useState(0);
  const { name, job, image, text } = people[index];
return (
    <article className="review">
      <div className="img-container">
        <img src={image} alt={name} className="person-img" />
        <span className="quote-icon">
          <FaQuoteRight />
        </span>
      </div>
      <h4 className="author">{name}</h4>
      <p className="job">{job}</p>
      <p className="info">{text}</p>
      <div className="button-container">
        <button className="prev-btn">
          <FaChevronLeft />
        </button>
        <button className="next-btn">
          <FaChevronRight />
        </button>
      </div>
      <button className="random-btn">
        Suprise Me!
      </button>
    </article>
  );
};
```


Next the functionality of the two chevron buttons is added to cycle the array indexes.
```React
        <button className="prev-btn" onClick={prevPerson}>
          <FaChevronLeft />
        </button>
        <button className="next-btn" onClick={nextPerson}>
          <FaChevronRight />
        </button>
   ```
   
   
   Now the two handler functions inside of the buttons have to be created.
   ```React
    const nextPerson = () => {
    setIndex((index) => {
      let newIndex = index + 1;
    });
  };
  const prevPerson = () => {
    setIndex((index) => {
      let newIndex = index - 1;
    });
  };
  ```


Now, once the reviews array reaches an index that doesn't exist an error will occur. To fix this error the checkNumber() function was constructed and added to the end of nextPerson() and prevPerson().
```React
  const checkNumber = (number) => {
    if (number > people.length - 1) {
      return 0;
    }
    if (number < 0) {
      return people.length - 1;
    }
    return number;
  };
  
    const nextPerson = () => {
    setIndex((index) => {
      let newIndex = index + 1;

      return checkNumber(newIndex);
    });
  };
  ```


Now the functionality is added to the random choice button.
```React
  const randomPerson = () => {
    let randomNumber = Math.floor(Math.random() * people.length);
    if (randomNumber === index) {
      randomNumber = index + 1;
    }
    setIndex(checkNumber(randomNumber));
  };
  ```
  
  Then finally render to the screen.
  ```React
  ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
  
