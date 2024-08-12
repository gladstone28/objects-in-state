[Link to coddecademy lesson](https://www.codecademy.com/courses/react-101/lessons/the-state-hook/exercises/objects-in-state)


### The State Hook

**Objects in State**

We can also use state with objects. When we work with a set of related variables, it can be very helpful to group them into an object. Let’s look at an example of this in action.
```
export default function Login() {
  const [formState, setFormState] = useState({});
  const handleChange = ({ target }) => {
    const { name, value } = target;
    setFormState((prev) => ({
      ...prev,
      [name]: value
    }));
  };

  return (
    <form>
      <input
        value={formState.firstName}
        onChange={handleChange}
        name="firstName"
        type="text"
      />
      <input
        value={formState.password}
        onChange={handleChange}
        type="password"
        name="password"
      />
    </form>
  );
}
```
A few things to notice:

- We use a state setter callback function to update a state based on the previous value.
- The spread syntax is the same for objects as for arrays: { ...oldObject, newKey: newValue }.
- We reuse our event handler across multiple inputs by using the input tag’s name attribute to identify which input the change event came from.

Once again, when updating the state with setFormState() inside a function component, we do not modify the same object. We must copy over the values from the previous object when setting the next value of a state. Thankfully, the spread syntax makes this super easy to do!

Anytime one of the input values is updated, the handleChange() function will be called. Inside this event handler, we use object destructuring to unpack the target property from our event object, then we use object destructuring again to unpack the name and value properties from the target object.

Inside our state setter callback function, we wrap our curly brackets in parentheses like so:
```
setFormState((prev) => ({ ...prev }))
```
This tells JavaScript that our curly brackets refer to a new object to be returned. We use ..., the spread operator, to fill in the corresponding fields from our previous state. Finally, we overwrite the appropriate key with its updated value.

Did you notice the square brackets around the name? This Computed Property Name allows us to use the string value stored by the name variable as a property key.
