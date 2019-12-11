## Filtering Input
This could be used as a search box. For example, get the State populated from an API:
```js
...
constructor() {
    super();
    this.state = {
      users: [],
      searchField: []
    };
  }

  componentDidMount() {
    fetch('https://jsonplaceholder.typicode.com/users')
    .then(response => response.json())
    .then(users => this.setState({ users }));
  }

  handleChange = e => {
    this.setState({ searchField: e.target.value.toLowerCase() } );
  }

  render() {
  
    const { users, searchField } = this.state;
    const filteredUser = users.filter(user => user.name.toLowerCase().includes(searchField));
    
    return (
      <div className="App">
        <SearchBox 
          handleChange={this.handleChange}
          placeholder='search users' 
        />
        <CardList users={filteredUser} />
      </div>
    );
  }
...
```
