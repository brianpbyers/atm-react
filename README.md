# ![GA LOGO](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67) React ATM application

Let's make an ATM app! You will practice the dark art of manipulating components in real time.  You will create two components of the same class which will work independently of each other.  

<img width="992" alt="atm" src="https://cloud.githubusercontent.com/assets/4304660/24376818/18c39a82-12f2-11e7-81e7-af618c22b3ed.png">


Clone this repo, and run `npm install` from inside it. The repo already includes a partial React app. To launch the app, run `npm start`.

### In `src/App.js`:
1. Pass a `name` property to each `Account` component, one for "Checking", the other for "Savings".  These will be used and accessed as `props`for our component. **Remember**: Props are immutable, that is, once they are declared, they cannot be changed while the application is running.

    <details>
    <summary>Click for code:</summary>

    ```javascript
        <div>
          <Account name="Checking"/>
          <Account name="Savings"/>
        </div>
    ```

    </details


### In `src/Account.js`

2. Use the property you set in `App.js` to add the name of the account to the `<h2>`.
    <details>
    <summary>Click for code:</summary>

    ```javascript
        <div className="account">
          //this.props.name is referring to the name property we assigned the App component in App.js
          <h2>{this.props.name}</h2>
          <div className="balance">$0</div>
          <input type="text" placeholder="enter an amount" />
          <input type="button" value="Deposit" />
          <input type="button" value="Withdrawl" />
        </div>
    ```

    </details>

    Save your work. You should see two components named Checking and Savings.  You're getting there!


3. Add a `balance` property to `state`, and set to 0 initially.
    <details>
    <summary>Click for code:</summary>

    ```javascript
        class Account extends Component {
            constructor(props){
              super(props)
              this.state = {
                balance: 0
              }
            }
        }
    ```

    </details>

<img src="https://media.giphy.com/media/26xBMuHu0ZFngH7Ta/giphy.gif">

> There are several ways to implement a form in React, here we took the approach as described in [these docs](https://reactjs.org/docs/forms.html).

4. Add a input value to the component state that is set to whatever value is typed into the text entry.

    <details>
    <summary>Hint:</summary>

    ```javascript
    this.state = {
      balance : 0,
      valueInput:''
    }

    // bind the "this" object to the handleChange function
    this.handleChange = this.handleChange.bind(this);
    
    ...
    
    handleChange(event) {
        this.setState({valueInput: event.target.value})
    }
    
    ...
    // attach the listener to the input
    <input type="text" placeholder="enter an amount" value={this.state.valueInput} onChange={this.handleChange}/>
    ```
    </details>

5. Add a function that adds the input value to the current balance when the user clicks 'deposit'

    <details>
    <summary>Hint:</summary>

    ```javascript
        // bind this object to the function
        this.handleDepositClick = this.handleDepositClick.bind(this);
        
        ...
        
        // define the function
        handleDepositClick(event) {

            this.setState({
              balance : parseInt(this.state.balance) + parseInt(this.state.valueInput),
              valueInput : ''
            })

        }

        ...
        // attach event listener
        <input type="button" value="Deposit" onClick={ (event) => this.handleDepositClick(event)}/>

    ```
    </details>

6. Add a function that subtracts the input value to the current balance when the user clicks 'withdraw'

    <details>
    <summary>Hint:</summary>

    ```javascript
        this.handleWithdrawClick = this.handleWithdrawClick.bind(this);
        
        ...
  
        handleWithdrawClick(event) {
            
            let newBalance = parseInt(this.state.balance) - parseInt(this.state.valueInput)
            
            if ( newBalance >= 0 ){            
                this.setState({
                  balance : newBalance,
                  valueInput : ''
                })
            } else {
                this.setState({
                  balance : 0,
                  valueInput : ''
                })
            }
        }

        ...

        <input type="button" value="Deposit" onClick={ (event) => this.handleWithdrawClick(event)}/>

    ```
    </details>


7. If the current balance is 0, you should add a class of `zero` to the `<div className="balance">`. You can complete these computations in the render method, but before the JSX portion is returned.
    <details>
    <summary>Hint:</summary>
        In the Account.js render method:

    ```javascript
      // set the default class to `balance` for the balanceClass.
      let balanceClass = 'balance';
      // if the balance is 0, then add the class zero to balanceClass
      if (this.state.balance === 0) {
        balanceClass += ' zero';
      }
    ```  

    <p>Replace the hardcoded `balance` class with the balanceClass variable in your return jsx code block:</p>

    ```html
        <div className={balanceClass}>$0</div>
    ```

    </details>
