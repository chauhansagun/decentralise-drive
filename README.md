# Decentralise-drive
PROJECT ARCHITECHTURE

1.Frontend - React JS
2.Backend - Solidity
3.Pinata - helps us to store images at IPFS
 (Because if we store imges on our smart contract that would be very heavy and expensive)
 Upload image -----------> get hash for that image ----------->get stored in your smart contract

Pre-requisites
1.Basic React
2.Ether.JS
3.Hardhat
4.Solidity
5.IPFS   

To know more about IPFS -> https://medium.com/geekculture/what-is-ipfs-the-inter-planetary-file-system-explained-40744a7ae95a

No database------humara smart contract(blockchain) he humara database hai

struct Access{
  address user;
  bool access; 
}

Here we will store the  url of images with respect to the address in array data form by using mapping.
-----> mapping(address=>string[]) value;
address--------->image URL


Here we will store the address of user who has access to the data in bool form by using mapping.
-----> mapping(address=>Access[]) accessList;
user------------>access

Variable that will tell us about the ownership with the hapl of Nested mapping(imagine it in the form of 2D Array).
Where rows and columns become your address.
----->mapping(address=>mapping(address=>bool)) ownership;

----->mapping(Address=>mapping(address=>bool)) previousData;
This will store the information about our previous data. We need this because we here we are not using Node.JS or any server and we are entirely dependent on our blockchain.


Mappings;

mapping(address=>string[]) value;
mapping(address=>mapping(address=>bool)) ownership;
mapping(address=>Access[]) accessList;
mapping(Address=>mapping(address=>bool)) previousData;


functions-

With the help of this function we are uploading the data of images w.r.t their URL.
function add(address _user, string memory url) external{
	value[_user].push(url);
}

Giving access to a particular user with his address
function allow(address useer) external{
	ownership[msg.sender][user]=true;
	if(previousData[msg.sender][user]{
		for(int i=0;i<accessList[msg.sender].length;i++){
			if(accessList[msg.sender][i].user==user){
				accessList[msg.sender][i].access=true;
			}else{
				accessList[msg.sender].push(Access(user,true));
				previousData[msg.sender][user]=true;   <----jab first time kissi ko allow krege
			}
		}
	} 
}

function to disallow a particular address from accessing the data after it is being allowed
function disallow(address user) public{
	ownership[msg.sender][user]=false;
	for(int i=0;i<accessList[msg.sender].length;i++){
		if(accessList[msg.sender][i].user==user){
			accessList[msg.sender][i].user==false;
		}
	}
}

here we are not deleting the address of the user because we can't do that as we are using blockchain we can change the data but cannot delete it entirely.












