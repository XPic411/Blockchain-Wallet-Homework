# Blockchain Wallet Homework: Cryptocurrency Wallet

## Task
Step 1: Import Ethereum Transaction Functions into the KryptoJobs2Go Application
Step 2: Sign and Execute a Payment Transaction
Step 3: Inspect the Transaction

## Instructions
### Step 1: Import Ethereum Transaction Functions into the KryptoJobs2Go Application

1. Review crypto_wallet.py script file. The Ethereum transaction functions that's built throughout this module—including wallet, wallet.derive_acount, get_balance, fromWei, estimateGas, sendRawTransaction, and others—have now been incorporated into Python functions that allow you to automate the process of accessing them.
2. Add mnemonic seed phrase (provided by Ganache) to .env file. Create .env file if needed.
3. Open the krypto_jobs.py file. Toward the top of the file, after the import statements that are provided, import the following functions from the crypto_wallet.py file: generate_account, get_balance, send_transaction

End Results:
from crypto_wallet import generate_account, get_balance, send_transaction

### Step 2: Sign and Execute a Payment Transaction

1. KryptoJobs2Go customers will select a fintech professional from the application interface’s drop-down menu, and then input the amount of time for which they’ll hire the worker. Code the application so that once a customer completes these steps, the application will calculate the amount that the worker will be paid in ether.

2. Write the code that will allow a customer to send an Ethereum blockchain transaction that pays the hired candidate. To accomplish this, locate the code that reads if st.sidebar.button("Send Transaction"). You’ll need to add logic to this if statement that sends the appropriate information to the send_transaction function (which you imported from the crypto_wallet script file). Inside the if statement.

End Results:
candidate_database = {
    "Lane": ["Lane", "0xaC8eB8B2ed5C4a0fC41a84Ee4950F417f67029F0", "4.3", 0.20,],
    "Ash": ["Ash", "0x2422858F9C4480c2724A309D58Ffd7Ac8bF65396", "5.0", 0.33,],
    "Jo": ["Jo", "0x8fD00f170FDf3772C5ebdCD90bF257316c69BA45", "4.7", 0.19,],
    "Kendall": ["Kendall", "0x8fD00f170FDf3772C5ebdCD90bF257316c69BA45", "4.1", 0.16,],
}

people = ["Lane", "Ash", "Jo", "Kendall"]

def get_people():
    db_list = list(candidate_database.values())

    for number in range(len(people)):
        st.image(db_list[number][4], width=200)
        st.write("Name: ", db_list[number][0])
        st.write("Ethereum Account Address: ", db_list[number][1])
        st.write("KryptoJobs2Go Rating: ", db_list[number][2])
        st.write("Hourly Rate per Ether: ", db_list[number][3], "eth")
        st.text(" \n")

### Streamlit application headings
st.markdown("# KryptoJobs2Go!")
st.markdown("## Hire A Fintech Professional!")
st.text(" \n")

### Streamlit Sidebar Code - Start
st.sidebar.markdown("## Client Account Address and Ethernet Balance in Ether")

### Step 2 - Part 1: 
Create a variable named `account`. Set this variable equal to a call on the `generate_account` function. This function will create the KryptoJobs2Go customer’s (in this case, your) HD wallet and Ethereum account.

account = generate_account()

st.sidebar.write(account.address)

##########################################
### Step 2 - Part 2:
Define a new `st.sidebar.write` function that will display the balance of the customer’s account. Inside this function, call the `get_balance` function and pass it your Ethereum `account.address`.

ether_balance =  get_balance(w3, account.address)
st.sidebar.write(ether_balance)

person = st.sidebar.selectbox("Select a Person", people)

hours = st.sidebar.number_input("Number of Hours")

st.sidebar.markdown("## Candidate Name, Hourly Rate, and Ethereum Address")

candidate = candidate_database[person][0]

st.sidebar.write(candidate)

hourly_rate = candidate_database[person][3]

st.sidebar.write(hourly_rate)

candidate_address = candidate_database[person][1]

st.sidebar.write(candidate_address)

st.sidebar.markdown("## Total Wage in Ether")

### Step 2 - Part 3: 
Write the equation that calculates the candidate’s wage. This equation should assess the candidate’s hourly rate from the candidate database (`candidate_database[person][3]`) and then multiply this hourly rate by the value of the `hours` variable. Save this calculation’s output as a variable named `wage`. Write the `wage` variable to the Streamlit sidebar by using `st.sidebar.write`.

wage = hourly_rate * hours

st.sidebar.write(wage)

##########################################
# Step 2 - Part 4:
Call the `send_transaction` function and pass it three parameters: Your Ethereum `account` information. (Remember that this `account` instance was created when the `generate_account` function was called.) From the `account` instance, the application will be able to access the `account.address` information that is needed to populate the `from` data attribute in the raw transaction. The `candidate_address` (which will be created and identified in the sidebar when a customer selects a candidate). This will populate the `to` data attribute in the raw transaction. The `wage` value. This will be passed to the `toWei` function to determine the wei value of the payment in the raw transaction. Save the transaction hash that the `send_transaction` function returns as a variable named `transaction_hash`, and have it display on the application’s web interface.

if st.sidebar.button("Send Transaction"):

    transaction_hash = send_transaction(w3, account, candidate_address, wage)

    st.sidebar.markdown("#### Validated Transaction Hash")

    st.sidebar.write(transaction_hash)

    st.balloons()

get_people()

### Step 3: Inspect the Transaction
In the terminal type "streamlit run krypto_jobs.py" to run the streamlit app

Take a screenshot of the address, balance, and transaction (TX) count. Save this screenshot to the README.md file of your GitHub repository for this Challenge assignment.
![image](./Images/Block_Content.png)

Navigate to the Ganache transactions tab and locate the transaction. Click the transaction and take a screenshot of it. Save this screenshot to the README.md file of your GitHub repository for this Challenge assignment.
