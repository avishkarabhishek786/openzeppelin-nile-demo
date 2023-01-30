# Openzeppelin Nile Devnet 

This is a step-by-step guide for [Openzeppelin Nile](https://docs.openzeppelin.com/nile/0.13.0/) 

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install cairo-nile.

```bash
mkdir testnile
Cd testnile
python3.9 -m venv mynile
source mynile/bin/activate
pip install cairo-nile

```

## Usage

```bash
nile init
nile compile
pytest tests/
nile node

# In .env file, paste 
ACCOUNT_1 = 0xAccount1PrivateKey  

# In new tab => 
source mynile/bin/activate

nile counterfactual-address ACCOUNT_1 --salt 123

# This will give the counterfactual address that needs to be funded by ether. 
# In devnet we can use OpenZeppelin script # to fund it. Create a new file called faucet.py in the scripts folder. # # # Paste the code to this file from this link - 
# https://docs.openzeppelin.com/nile/0.13.0/scripts#transfer_funds_from_a_predeployed_devnet_account and change the 
# receiver address to the counterfactual address.

nile run scripts/faucet.py
nile get-balance 0xCounterfactualAddress

# Now declare ACCOUNT_1. Create a file scripts/declare_oz_account.py and copy the code from 
# https://docs.openzeppelin.com/nile/0.13.0/scripts#declare_account to this file.

nile run scripts/declare_oz_account.py
nile setup ACCOUNT_1 --salt 123 --estimate_fee
nile setup ACCOUNT_1 --salt 123 --max_fee 506300000000000
nile declare ACCOUNT_1 contract
nile deploy ACCOUNT_1 contract --alias my_contract
nile call my_contract get_balance
nile send ACCOUNT_1 my_contract increase_balance 2
nile call my_contract get_balance

```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.