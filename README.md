# Tan
1.)To add "Check if a user is registered" this feature:
I made the following function in solidity file-
function isRegistered(address _addr) public view returns (bool) {
    return people[_addr].walletAddress != address(0);
}
To fetch the corresponding button , I made some code fixes in app.js file -
Added these useState:
const [checkAddress, setCheckAddress] = useState('');
  const [checkResult, setCheckResult] = useState(null);
  
Added this function :
const handleCheckRegistration = async () => {
    if (!contract || !checkAddress || !ethers.utils.isAddress(checkAddress)) {
      alert("Please enter a valid Ethereum address.");
      return;
    }
  
    try {
      const person = await contract.getPerson(checkAddress);
      const isRegistered = person.walletAddress !== ethers.constants.AddressZero;
      setCheckResult(isRegistered);
    } catch (error) {
      console.error("Error checking registration:", error);
      alert("Failed to check registration.");
    }
  };

  Added this for the frontend button:

<div style={{ marginTop: '30px' }}>
  <h3>Check If Address is Registered</h3>
  <input
    type="text"
    placeholder="Enter Ethereum address"
    value={checkAddress}
    onChange={(e) => setCheckAddress(e.target.value)}
    style={{ width: '350px', marginRight: '10px', padding: '5px' }}
  />
  <button onClick={handleCheckRegistration}>Check Registration</button>

  {/* Result Message */}
  {checkResult !== null && (
    <p style={{ marginTop: '10px', fontWeight: 'bold', color: checkResult ? 'green' : 'red' }}>
      {checkResult ? '✅ True' : '❌ False'}
    </p>
  )}
</div>

2.) To add "Display connected wallet address" feature :
Added this code in app.js file:
{isConnected && (
  <p style={{ marginTop: '10px', color: '#00FF00' }}>
    Connected Wallet: {account.substring(0, 6)}...{account.substring(account.length - 4)}
  </p>
)}

3.) To add "Display total registered users" feature , added the code in app.js file:
{/* PEOPLE LIST - Show all registered users */}
            <h3>People</h3>
            <p>Total Registered Users: {people.length}</p>

        
