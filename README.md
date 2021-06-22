# settlementIO - 1.1
Creating and trustful judgment system

As decentralized world grows, we see a growth on scams and robbery being leverage by ICO's and obnoxious lack of certification of the new networks and cryptocurrencies provides as a security to it's donors and owners, we lack trust , but not trust by the state, but trust by the network.
We can see cases of adopters of cryptos complaining that their were scammed, and lost all their money , because they went to a hype of some crypto, and at the end were a scam.
The decentralized world yet didn't came out with a system that uses decentralization to resolve the disputes among Institutions, networks and users, making this ecosystem a open field for those who wants to harm others , the growing decentralization will need new ways to solve a dispute, or rely on future regulations created by government, and we don't want that.

So, in order to bring settlement disputes to a decentralized world , a new approach for this issue needs to be created.

## Goal

The goal of settlementIO it's to create a DAO(Decentralized Autonomous Organization) using a settlement algorithm described on this paper , where a certificate/insurance can be issued by a institution to ensure disputes to be resolved on a distributed level, using smart contracts where a dispute can be issued, reviewed and the result recorded , using digital signature, third party reviewers and law abide owners.
To achieve this Goal , the  settlement algorithm that contentIO will use it's called `Punitive Proof-of-Adequacy`.

## 1. Punitive Proof-of-Adequacy

The punitive Proof-of-Adequacy is a settlement algorithm protocol that operates on top of a blockchain-based smart contract network that aims to use a distributed consensus to achieve a result on a **settlement** dispute. The PoA protocol is an earlier level of consensus, where the peers connected to the network can act creating a network channel ( a Pool ) , assigning an odd _n_ P2P curators([Reviewers](#33-Reviewer)) connected to the network, giving them access on a **settlement** dispute via a combination of random selection of [Reputations](#Reputation), thus generating a smart contract of the result of the dispute , using the fees to be shared among peers curators and the creator, known as [Witness](#Witness), of the next contract.

In able to record on a blockchain, PoA will use a [Witness](#Witness) , a node to index the results on a smart contract-based network, as ETH being the chosen platform for the testnet.

### 1.0 Pre dispute: the institution assignments

As tough before, disputes could be created by a peer or institution against any peer and/or institutions.

But to generate smart contracts and automatically enforce them was a flaw on the `V1.0` of this white paper.

On the proposal of `V1.1` settlementIO will hold dispute only by institutions assigned to the network

#### 1.0.1 How will the institutions connect with SettlementIO network


SettlementIO will provide a set of Apis where institutions and network will be able to connect themselves to the SettlementIO network.

Networks and DAO or other institutions can connect with ContentIO adding a document known as `Dispute terms` , highlighting the terms of agreement with them with any future contracts. The institutions will pay a fee to `mint` the terms on a `dispute pool`.

The `dispute pool` is a hodl wallet where can be used when a result of a dispute  enforces the institution to pay reparations to the complaint.

ContentIO issue a signed document, approving signed institution to ContentIO network.

### 1.1 Process

When a [Reporter](#Reporter) file a **settlement** against the [Appealer](#35-appealer) , the Issuer(_I_) recieve the dispute, then sends to the 
network the **settlement** to be reviewed(_r_), at this moment a [bounty](#Bounty) can be issued. It's from the discreet 
of the [_I_](#31-issuer) to notify the Appealed of the **settlement** dispute in course, if don't, 
it must be send the information.
eg.: 
```javascript
settlementIssued = {
    data : `<SETTLEMENT PROCESS>`,
    issuer: '688A044D54361D5762100BD1E6559AF4',
    reporter: '4A12FE7C3773A2B801BFFEB341A77949',
    appealer : '39AAF3FEF253178E15963B9CC27DA138'
}
```
The request it's sent to a Assigment Pool , where the Issuer will accept a number(_n_) of _r_ , where this _n_ it's a odd quantity of minimum of 7, to a maximum of 25 of _r_, 
who requested to be assigned to review the content issued. The _r_ assigned to the content to be reviewed are 
designated based on the following :

- Position on the assignment pool
- Reputation
- Waiting time

After the designation, the content receive a feedback of the _n_ assigned peer _R_, and the final [result](#Result) it's settled.
 The [Result](#Result) then it's sent back to PoA algorithm to record it on a blockchain. 

The PoA send a data to a [pool of results](#pool-of-results), to be recorded on a blockchain. The data must contain: 
- The Review reference/data [Result](#Result) of the settlement 
- The price distribution among the winners of the voting settlement added 60% of the [bounty](#Bounty) issued and 
reduced by the [Witness](#Witness) fee `G = pd + (b? b*(60/100) : 0) - wf`, if there is any.
- The Witness Total settlement fee attached to 40% fo a [bounty](#Bounty) issued `SF = wf + (b? b*(40/100): 0) `, if there is any, 
- The hash of all [reviewers](#33-Reviewer) which was on the settlement 
- The hash of the writing witness.

```javascript

settlementResult = {
  RR: '4A12FE7C3773A2B801BFFEB341A77949',
  G : `${pd + (b*(60/100) - wf)}`,
  SF : `${wf + (b*(40/100))}`,
  RW : ['CC54BD37BED550B4F756284A9FF42B4E', '79E9BBAE4E3C33C4EC16E1CCB303EE0B', 'CD47C54AFED2B25F833610FDB8875908', 
  '0AFB3728EC8AEB70B2B13FB1B6E714E2', '39AAF3FEF253178E15963B9CC27DA138', '92238FEAF3A982CF7D42D6C8FB52D804', 
  '688A044D54361D5762100BD1E6559AF4'],
  W: 'F56146D752AA1B96CB455B59FC017FD9'
}

```

> G is the total Grant of the [Result](#Result), pd = price distribution, b = bounty , SF = [Witness](#Witness) settlement fee, wf = [Witness](#Witness) fee

A [Witness](#Witness) it's assigned to generate a block on the blockchain via PoS, PoW or the 
[Witness](#Witness) Assignment Logic. Then it will take _n_ data from the [pool of results](#pool-of-results) and 
record it on the blockchain


#### 1.1.1 In a nutshel :

![](images/nutshell2.png "Parent block")

> 1 - A dispute is made to the network following a certain rule it’s being request.
> 2 - One peer of the network , defined as Issuer, will register the dispute and request to other peers to be assigned.
> 3 - Peers request to assign as a Reviewer to the dispute, and a odd number of Reviewers will be chosen by the issuer.
  4 - Peers granted the availability it will be sorted by their reputation on the network.
  5 - Reputations are defined on the previous actions the peers made.
  6 - The result generates a Smart Contract.
  7 - The dispute results it’s informed back.


### 1.2 Appeal
A Appeal of the [Result](#Result) can be issued and restart the process , generating a new data to be recorded on the 
block referring the hash of the last [Result](#Result). 

If the result it's the same, the **settlement** it's closed and It can't be Appealed again(appealFowardResult). 

If the Appeal it's giving a different result, but the algorithm request a another appeal process to be retrieve the 
result of the Issuer. Depending of the result, it's fires the punitive algorithm which will reduce the **Reputation** and 
a charge fee to be deducted of the loosing peer reviewers, adding the charge on the prize of the next **settlement** 
dispute of the Issuer(appealBlockingResult). 

The reviewers charged can't appeal, as they aren't one of the 3 p2p actors with this level of permission.

```javascript

appealFowardResult = {
  LR: `F56146D752AA1B96CB455B59FC017FD9`,
  RR: '4A12FE7C3773A2B801BFFEB341A77949',
  G : `${pd + (b*(60/100)) - wf}`,
  SF : `${wf + (b*(40/100))}`,
  RW : ['CC54BD37BED550B4F756284A9FF42B4E', '79E9BBAE4E3C33C4EC16E1CCB303EE0B', 
  'CD47C54AFED2B25F833610FDB8875908', '0AFB3728EC8AEB70B2B13FB1B6E714E2', '39AAF3FEF253178E15963B9CC27DA138', 
  '92238FEAF3A982CF7D42D6C8FB52D804', '688A044D54361D5762100BD1E6559AF4'],
  W: 'F56146D752AA1B96CB455B59FC017FD9'
}

```

```javascript

appealBlockingResult = {
  WR: '39AAF3FEF253178E15963B9CC27DA138',
  LR: 'F56146D752AA1B96CB455B59FC017FD9',
  RR: '4A12FE7C3773A2B801BFFEB341A77949',
  G : `${pd + (b*(60/100)) - wf}`,
  SF : `${wf + (b*(40/100))}`,
  RW : ['CC54BD37BED550B4F756284A9FF42B4E', '79E9BBAE4E3C33C4EC16E1CCB303EE0B', 'CD47C54AFED2B25F833610FDB8875908', 
  '0AFB3728EC8AEB70B2B13FB1B6E714E2', '39AAF3FEF253178E15963B9CC27DA138', '92238FEAF3A982CF7D42D6C8FB52D804', 
  '688A044D54361D5762100BD1E6559AF4'],
  W: 'F56146D752AA1B96CB455B59FC017FD9'
}

```


### 1.3 Assignment pool

When a _R_ request a **settlement** for a review , the Issuer will gets the first [reviewer](#33-Reviewer) available 
on the Pool (_P_) of assigment and ask for a review, then the [reviewer](#33-Reviewer) it's sent to the end of the _P_.
The position on the assigment pool are defined by time connected on the network, and the position is distributed among the peers. 
Having the top position on the Assigment Pool doesn't automatically grants the  [reviewer](#33-Reviewer) the assigment from the Issuer,
it's only a another measurement used to define the assignee of a dispute.


> `_A_ = _I_.get((reviewer) => reviewer.position )`

#### 1.3.1 Assignment Ordination
In order to keep the pool assignment with the must trustful result as possible, the [Reputation](#14-reputation) of 
_n_ _R_ should be differentiated, getting the advantage of distributing _n_ assignees on a single review by a range 
of experienced _R_ to new one(or still pooly trustable) on the peer network. This range are defined by the _R_ 
reputation (defined on section [Reputation](#reputation)). To control and maintain the trustful of the network the 
votes will be weight by the assignee reputation, giving the system a controlled and better results of the reviews.
Doing that, the aiming it's to avoid misleading engagement or vicious behaviour from more experienced peer users, avoid 
power centralization among the reputation peers, and give a more honest result of the review.
The weight of the votes it's referred on the [Vote System Weight](#vote-system-weight) section.

### 1.3 Bounty

Bounty it's a additional fee inserted on the **settlement** dispute , created to enable the possibility of a Issuer to 
require a faster result on a dispute it's generated. A dispute with an added bounty it gains priority on top of any other 
dispute on the network.

### 1.4 Reputation

A Range of reputation(_rp_) it's given to the _R_ , these are "Trustful", "MidLevel", "Non-Trustful" and "Undesirable".
 When a new _R_ it's created, a "Non-Trustful" level it's assign to it's status. The more engaged 
 
### 1.5 Waiting time 

While in the pool, the _R_ will record it's waiting time, which means the time it connected to the network and hasn't been granted a assigment.
The waiting time is a metric used when a Issuer recieves request of assigment of the peers _R_

### 1.6 Vote System && Weight

The [reviewer](#33-Reviewer) will recieve the **settlement** and the _I_ rules and define if the **settlement** it's on 
favor or against the [Reporter](#Reporter). After the [reviewer](#33-Reviewer) gives it's vote, the _I_ will 
require for the next assignee [reviewers](#33-Reviewer) on the _P_, having this [reviewer](#33-Reviewer) a different 
level of [Reputation](#Reputation)(as seen on [Assignment Ordenation](#121-assignment-ordenation)). After the minimum 
of 7 votes, the algorithm checks if the **settlement** have a result, if not it will assing another 
[reviewer](#33-Reviewer) until the next odd _n_ of votes and check for the result, having this behaviour until _n_ of 
votes it's 25.   
This _P_ it's responsible to queue the assignees to be assign to a next **settlement**. The quantity of _R_ to be 
assigned(_A_) will be the minimum of 7, to a maximum of 25.

A _A_ must have assignees distributed on the following reputation  : _R_['Trustfull'] = 25% , _R_['MidLevel'] = 30%, 
_R_['Non-Trustfull'] = 45%. The reputation defines the power of the vote of each assignees. The "Non-Trustful"(_ntt_) 
it's the benchmark voter, where "MidLevel" has `1.5*ntt` vote power , and the "Trustful" _R_ having `2.5*ntt` vote 
power.

### 1.7 Result

The result of a dispute will generate a Smart Contract to be recorded.

### 1.8 Pool of Results

All the results will be queue on a pool to be consumed.

### 1.9 Reputation gratifications/punishment

After the result it's defined , the Reputation algorithm it's fired, analysing the voters and the outcomes of the result.
When analysed, the algorithm it grants the gratification, which is gave by taking the total fee and spreading the value 
to the winner voters and the amount divided by the peers Reputation.

### 1.10 Benefit of doubt
A **settlement** dispute must have a trustful result, and for that, a **settlement** have to be reviewed by a odd `n` 
of [Reviewers](#33-Reviewer)(_R_). To ensure a result it's trustful, the algorithm allow the 
[benefit ouf doubt](#benefit-of-doubt) of any **settlement** result, and this doubt it's granted to the 3 p2p actors. 
They are the 2 parts on the dispute, the [Reporter](#Reporter) and the [Appealer](#Appealer), and the law abiding 
[Issuer](#31-issuer), who defines the [rules](#rules-of-the-settlement) where a **settlement** dispute is going on. 
The amount of [benefit ouf doubt](#benefit-of-doubt) it's determined by it's own cryptocurrency blockchain network, 
but in able to avoid fraud it's recommended to follow the instructions on this paperwork.


## 2. Rules of the settlement

The Rules of the settlement it's defined by the [Issuer](#Issuer), so the PoA defines this actor the single source of 
truth when a [Benefit of doubt](#110-benefit-of-doubt) it's on.

## 3. Actors

### 3.1 Issuer
It's the peer who has access to the PoA network to send the **Settlement** dispute over the pool of assigment and accept [Reviewers](#33-Reviewer) request to it. The Issuer can be either the Reporter, 
Appealer or a network access holder, such as companies who wish to create their private PoA network. 


### 3.2 Reporter

Who's generate the dispute to be distributed by the Issuer.

### 3.3 Reviewer 
The first `n` users connected to the platform who selfAssign the review lock the analysis of that content and give 
their result, the distribution of the review it's held by the **Witness**, who assign the review on the pool and check 
the  **Reviewer** `poor-of-integrity`, based on the issuer internal policies. The users can't know each others , so 
that the system works a non-trustful nodes.

### 3.4 Witness
The **Witness** it's the algorithm(miner) which will hold the distribution of the **Issuer** content for review trough 
the **Reviewers** , defined by `location` , `reputation`, `proof-of-stake`. Once the **Reviews** are issued, **Witness**
 algorithms take the reviewers result, and record the content result on the **Chain**, working as a notary book for 
 consultation by the **Issuer**. Therefore the prize value are divided between the **Reviewers** and credit on their
  account, which will be paid monthly/weekly. A **Witness** node who insert the **Review** first it's granted the fee 
  charged from the **Issuer**. The **Issuer** can be a **Witness** for the chain.

### 3.5 Appealer
Users/reporters who have a **settlement** result against their will, can appeal te result of the review and a new
 request are issued. _n_ appeals can be granted by **settlement** , defined by default of by the **Issuer**. It's 
 from the discreet of the _I_ to notify the Appealer of the **settlement** dispute in course, but the Appealer must 
 be notified after the result. And the _I_ must inform the network if the Appealer were notified when the **settlement** 
 dispute were post in course


## 4. Security measurement
How to secure the block


## 5. Pros
Company can use the platform where the pool of nodes to be reviewed can give more returns for the content **Reviewers**
Platform can be `onPrem` or `onCloud`.
**Reviews** can be more reliable.

## 6. Cons

Who review the **Reviewer**

Develop how the platform will receive the content from the **Issuer** and deliver it to the **Reviewer**

Define how a appeal must be accepted by a **Reviewer**. A `punitive proof-of-adequacy` must be implemented in full to
 enforce the need of the reviewer be trustful on his/her review(also can work for managing the user behaviour)



