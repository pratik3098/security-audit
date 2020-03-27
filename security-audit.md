## Bad Kickback Security Audit Report

## 1. Disclaimer
Not guarantee bug free

## 2. Summary
Bad Kickback security audit performed by:
    Name: Pratik Patil
    Student Id: 101284380
    
Source: https://github.com/ethereumgb/security-audit


## 3. Scope
1. BadKickback.sol

## 4. Findings

In total, 7 issues were reported including:

  * 1 critical severity issue.

  * 2 high severity issues.

  * 2 low severity issues.

  * 2 owner privileges (the ability of an owner to manipulate contract, may be risky for investors).

## 4.1. Self destruction vernability
 #### Severity 
  owner privileges
 #### Description
  Anyone is allowed to call the self destruction function. 
  Selfdestruction of the callee contract can leave callers in an inoperable state.
  
 #### Code snippet
 Line 56.

 #### Recommendation
  Add the following code to the destroy() function:
  require(owner== msg.sender);

## 4.2. Gas requirement of payout function
  #### Severity
   critical

  #### Description
  If the gas requirement of a function is higher than the block gas limit, it cannot be executed.

  #### Recommendation
  The problem can be fixed by storing the attendees addresses in an array instead of mapping.

## 4.3. Static variable is not constant 
  #### Severity
    low

  #### Description
   The constant variable "cap" is not declared as a constant.
 
  #### Code snippet
   Line 17.

## 4.4. Delegate call can manipulate owner privilage
 #### Severity
  owner privileges
 #### Description
   By using the delegate call functionality, the owner address can be manipulated to (msg.sender).
  
 #### Code snippet
   Line 23.

## 4.5. Improper payout calculation
 #### Severity
   High

 #### Description
   The payout amout is being calculated without precision.

 #### Code snippet
   Line 43.


## 4.6. Payout loop break
 #### Severity
   High

 #### Description
   The payout loop is break and exited if one of the address is not in the participants list. 
   Thus, leaving the other participants without any payout.

 #### Code snippet
   Line 47, 48.


## 4.7. delegate call  can manipulate fee
 #### Severity
   Low
 #### Description
   The event fee is not constant, thus, leaving the vulnerability of modifying it.

 #### Code snippet
   Line 20.



## 5. Conclusion
The contract contains the dangerous vulrenabilties which needs to be fixed before deployment, If the contract contains constructor, most of the issues can be resolved easily.
