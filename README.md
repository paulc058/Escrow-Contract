// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
contract Escrow{
    address public buyer;
    address public seller;
    address public escrowAgent;
    uint256 public AnountDeposited;
    uint256 public deadline;
    bool public DilveryConfirmed;
    }
    enum State{Waitingforpayment, waitingforDilveryConfirmation,completed,Refunded}
    State public CurrentState;
    modifier onlyBuyer(){
        require(msg.sender == buyer, "Only the buyer can execute");
        _;

    }
    modifier onlySeller(){
        require(msg.sender == EscrowAgent, "Only the escrow agent can execute");
        _;

    }
    modifier InState(State _state){
        require(currentState == _state, "Invalid state for request");
        _;
    }
    //the constructor to contract the seller, buyer and escrow agent
    constructor(address _seller, address _buyer, address _EscrowAgent,
    uint256 Deadline){
        Deadline = _Deadline;
        EscorwAgent = _EscrowAgent;
        Buyer = _Buyer;
        Seller = _Seller;
        Waitingforpayment = current.state;


    }
    //For the buyer to deposit the funds into the contract
    function Deposit() external payable onlybuyer{
        inState(WaitingforPayment.state)
        require(msg.value >0, "The deposit must be greater than zero Ether");
        State.WaitingforDilveryPayment = Current.state;
        msg.value = AmountofEtherDeposited;
              
    }
    //The function that the buyer confirms that the good/service has been dilivered
    function confirmDilvery() external onlyBuyer{
        (State.WaitingForDiliveryConfirmation)inState;
        DiliveryConfirmed = true;
        releasepayment();
        State.completed = Current.State;
        
    }
    //If the conditions are met, the funds can be transferred to the seller from
    //the Escrow agent
    function ReleasePayment() internal{
        require(amountDeposited>0,"Amount of ether has not been released yet");
        require(DiliveryConfirmed,"The dilivery has not been confirmed yet");
        State.completed = Current.State;
        payable(seller).(amountDeposited).transfer;
        }
        //the function for the buyer to request a refund before the deadline
    function RequestRefund() external onlyBuyer{
        (State.WaitingforDiliveryConfirmation)inState;
        require(!diliveryConfirmed,"Dilivery has not yet been confirmed");
        require(block.timestamp<=deadline,"The refund period has expired");
        amountDeposited = 0;
        uint256 RefundAmount = AmountofEtherDeposited;
        State.refunded = currentState;
        transfer(Refundamount).payable(buyer);
        
    }
    //the function to check the current state of the smart contract
    function GetState() external view returns (bool){
        return.block.timestamp> deadline;

    }
    //the function to check if the contract has expired
    function hasExpired() external view returns(bool){
        return CurrentState;
    }
    //To See the current balance of the smart contract
    function GetBalanceofContract() external view returns(uint256){
        return.address(this).balance;
        
    }
