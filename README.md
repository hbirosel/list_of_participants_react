# list_of_participants_react
list_of_participants_react
var totalVec = new Array();

function Header(){
  return (
    <h1>List of Participant</h1>
  )
}

var ListItem = React.createClass({
    getInitialState: function(){
      return {name: this.props.value.product.name, email: this.props.value.product.email, phone: this.props.value.product.phone, totale: 0} 
    },
  
    render: function(){
    return(
      <tr>
        <td><input type="text" name="name" value={this.state.name} onChange={this.handleChange} placeholder="Full Name..."/></td>
        <td><input type="text" name="email" value={this.state.email} onChange={this.handleChange} placeholder="Email Address..."/></td>
        <td><input type="text" name="phone" value={this.state.phone} onChange={this.handleChange} placeholder="Phone Number..."/></td>
        
      </tr>
    )
  },
    
  handleChange: function(event){
    const target = event.target;
    const name = target.name;
    const value = target.value;
    
    this.setState({
      [name]: value
    }, this.calcoloTotale);
  },
  
  
  
  
 
});
  
  
var Table = React.createClass({
  getInitialState: function(){
    return { totale: 0 } 
  },
  
  render: function(){
    return(
      <div>
        <table>
          <tr>
            <th>Name</th>
            <th>Email</th> 
            <th>Phone</th> 
       
    </tr>
          {this.props.items.map((prodotto) =>
            <ListItem key={prodotto.id} value={prodotto} />
          )}
         
        </table>
      </div>
    )
  },
  
  updateGlobalTotal: function(){
    var total = 0;
    for(var i = 0; i < this.props.ids; i++){
      total += totalVec[i];
    }
    
    
  }
  
});

var AddNewRow = React.createClass({
  render: function(){
    return(
      <div>
        <button onClick={this.props.onClick}>+</button>
        Add Data
      </div>
    )
  }
});

var Data = React.createClass({
  getInitialState: function(){
    return {
      counter: 2, lists: [{ product: {name: "",email: "",phone: ""}}, 
  {id: "1", product: {name: "",email: "",phone: ""}}]
    }
  },
  render: function(){
    return (
      <div className="container">
        <Header />
        <Table items={this.state.lists} ids={this.state.counter}/>
        <AddNewRow onClick={this.addRow}/>
      </div>
    )
  },
  
  addRow: function(){
    this.setState({counter: this.state.counter + 1});
    var listItem = {id: this.state.counter, product:{name:"", email: "", phone: ""}};
    var allItem = this.state.lists.concat([listItem])
    this.setState({lists: allItem});
  }
});

ReactDOM.render(
  <Data />,
  document.body
);


