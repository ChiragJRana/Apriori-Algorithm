# Apriori-Algorithm For Market Basket Analysis
![MarketBasket](https://user-images.githubusercontent.com/42936626/103854640-f6df8800-50d6-11eb-80a4-9fd55574cf95.jpg)

## Introduction

What is **Market Basket Analysis**?

MBA a technique used by large retailers to uncover associations between items. It works by looking for combinations of items that occur together frequently in transactions, providing information to understand the purchase behavior.<br />
The outcome of this type of technique is, in simple terms, a set of rules that can be understood as “if this, then that”.<br />
It inludes some statistical concepts  like support, confidence, lift to select interesting rules.<br /><br /><br />

## **Association Rules**
The Apriori algorithm generates association rules for a given data set. An association rule implies that if an item A occurs, then item B also occurs with a certain probability.</br>
For example:

Transaction | Items
------------ | ------------- 
t1	| {T-shirt, Trousers, Belt}
t2	| {T-shirt, Jacket}
t3	| {Jacket, Gloves}
t4	| {T-shirt, Trousers, Jacket}
t5	| {T-shirt, Trousers, Sneakers, Jacket, Belt}
t6	| {Trousers, Sneakers, Belt}
t7	| {Trousers, Belt, Sneakers}
</br>

In the table above we can see seven transactions from a clothing store. Each transaction shows items bought in that transaction. We can represent our items as an **item set** as follows</br>

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  *I={i1,i2,...,ik}*

In our case it corresponds to:</br>
##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; I={T-shirt,Trousers,Belt,Jacket,Gloves,Sneakers}

A transaction is represented by the following expression:

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; T={t1,t2,...,tn}

For example,
##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; t1={T-shirt,Trousers,Belt}

Then, an association rule is defined as an implication of the form:

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; X⇒Y, where X⊂I, Y⊂I and X∩Y=0

For example,

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {T-shirt,Trousers}⇒{Belt}

In the following sections we are going to define four metrics to measure the precision of a rule.

## **Support**
Support is an indication of how frequently the item set appears in the data set.

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; supp(X⇒Y)=(|X∪Y|)/(n)

In other words, it’s the number of transactions with both X and Y divided by the total number of transactions. The rules are not useful for low support values. Let’s see different examples using the clothing store transactions from the previous table.

* ### supp(T-shirt⇒Trousers)=3/7=43%
* ### supp(Trousers⇒Belt)=4/7=57%
* ### supp(T-shirt⇒Belt)=2/7=28%
* ### supp({T-shirt,Trousers}⇒{Belt})=2/7=28% </br>

## **Confidence**
For a rule X⇒Y, confidence shows the percentage in which Y is bought with X. It’s an indication of how often the rule has been found to be true.

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conf(X⇒Y)=(supp(X∪Y))/(supp(X))

For example, the rule T-shirt⇒Trousers has a confidence of 3/4, which means that for 75% of the transactions containing a t-shirt the rule is correct (75% of the times a customer buys a t-shirt, trousers are bought as well). Three more examples:

* ### conf(Trousers⇒Belt)=(4/7)/(5/7)=80%

* ### conf(T-shirt⇒Belt)=(2/7)/(4/7)=50%

* ### conf({T-shirt,Trousers}⇒{Belt})=(2/7)/(3/7)=66%

## **Lift**
The lift of a rule is the ratio of the observed support to that expected if X and Y were independent, and is defined as

##  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lift(X⇒Y)=(supp(X∪Y))/(supp(X)supp(Y))

Greater lift values indicate stronger associations. Let’s see some examples:

* ### lift(T-shirt⇒Trousers)=(3/7)/((4/7)(5/7))=1.05

* ### lift(Trousers⇒Belt)=(4/7)/((5/7)(4/7))=1.4

* ### lift(T-shirt⇒Belt)=(2/7)/((4/7)(4/7))=0.875

* ### lift({T-shirt,Trousers}⇒{Belt})=(2/7)/((3/7)(4/7))=1.17

To view My analysis and implementation of Apriori algorithm open the file **Apriori Learning algorithm From scratch.ipynb** :star_struck:

I have used the dataset provided by SuperDataScience on Udemy.