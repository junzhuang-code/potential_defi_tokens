# The Next Potential Defi Token To The Moon
(1561 words, 6m14s reading time)

#### Author: Jun Zhuang

### What is Defi?
[Decentralized Finance](https://en.wikipedia.org/wiki/Decentralized_finance), namely Defi, is new emerging terminology for a variety of financial applications or services based on the blockchain platform. The goal of Defi is to establish a financial system that opens to every user. To fulfill this goal, Defi leads to the bull market in recent months. Most existing Defi services can be divided into five categories: Lending, DEXes, Derivatives, Payments, and Yield farming.  
* **Lending** is similar to the bank. Users can borrow money from this project or deposit the money here to earn interest. However, unlike the bank, this kind of lending project does not need to monitor the users by a human. All rules are executed by the smart contract.
* **DEXes** is short for Decentralized Exchanges. It's a kind of crypto exchange that allows everyone to buy or sell all kinds of tokens.
* **Derivatives** is a promising direction of Defi as it provides many derivative tools to professional investors to hedge the risk.
* **Payments** here may refer to the Bridge across different blockchains. For example, users from Ethereum could transfer their assets to Binance Smart Chain (BSC) or Huobi Ecosystem (Heco), or vice versa.
* **Yield** is short for yield farming, which refers to a kind of project that provides high yield products to investors. For example, the project admin could design a smart contract to help investors auto-compound the stacked tokens in DEXes and then earn the performance fee.


### How do we find out the next potential Defi token to the moon?
Many popular Defi projects offer tokens. Investors can buy the token for investment purposes. Indeed, some famous Defi tokens have a great increase in this bull market. Many investors may want to find out the next potential Defi token that will launch to the moon to maximize their profit. However, it is a challenging problem that nobody can guarantee this kind of token. To embrace this challenge, I design a scheme to find out such tokens by machine learning approaches.

**Data Collection**  
At first, I collect a demo dataset from several famous cryptocurrency websites, such as [Defipulse](https://defipulse.com/), [Coinmarketcap](https://coinmarketcap.com/), and [Defibox](https://www.defibox.com/index). After that, I select features and label the data based on the return. More specifically, I split the return into three earning levels (1,2,3). I label the data as the high earning level when the token got the return no less than 1,000% in 2021 (to Apr. 26), whereas I label the data as the low earning level when the token got the return less than 400% in the same period. The rest data is labeled as the medium earning level. The ratio of these three levels is 8:7:5 (from low to high). The intuition is that we want to find out which token has a higher return. To do so, I convert this problem into a classification task.

Besides, I make a brief introduction to the selected features as follows.
* Name (Str): The name of the Defi project.
* Symbol (str): The symbol of the token.
* Chain (str): The blockchain that the project first deploys.
* Category (str): The Category that the project belongs to.
* TVL (float): Total value locked refers to the total money (USD in billion) that investors deposit in the project.
* Mkt_Cap (float): The market capitalization of the token (USD in billion).
* MC/TVL (float): The ratio of Mkt_Cap to TVL.
* Cir_Supply (int): The number of tokens that are circulating in the market and are in public hands.
* Total_Supply (int): The number of tokens that have been already created, minus any coins that have been burned.
* Max_Supply (int): The maximum number of tokens that will ever exist in the lifetime of the cryptocurrency.
* Cir_Ratio (float): The ratio of the circulating supply to the total supply.
* Price0 (float): The price (USD) on the first day or in 2021-01-01 (Applied to the earlier one).
* Price1 (float): The price (USD) on the collection day (2021-04-26).
* Return (float): The ratio of Price1 to Price0, which indicates the return.

![image](https://github.com/junzhuang-code/potential_defi_tokens/blob/main/images/tvl.png)  
Total value locked (USD) in Defi increases from 30B to more than 60B in only 90 days (from Defipulse). It indicates that investors have a high passion to embrace the Defi. The bull market is mainly driven by Defi.  

![image](https://github.com/junzhuang-code/potential_defi_tokens/blob/main/images/mc.png)  
The total market capitalization rapidly increases in the recent four months (from Coinmarketcap).    

**Preprocessing**  
After building the dataset, I implement one-hot embedding on *'Chain'* and *'Category'* as these two features are categorical strings. After that, I drop some unnecessary features such as *'Name'* and *'Symbol'* since these two features are unique to each token and have no help to our task. Lastly, all values are normalized within [0, 1] for better training.

**Methods**  
Until now, we can employ machine learning models to classify the data. In this demo, I select two classic models, random forest classifier (RFC) and support vector machine classifier (SVMC). Before training the models, I split the dataset as train data (75%) and test data (25%). Also, I evaluate the performance by accuracy on the test data. Duo to demo purpose, I didn't tune the models. The results show that both models achieve **80%** accuracy, which means that this design can successfully find out the tokens from each earning level.

| Model | Accuracy |
| :-----: | :----: |
| RFC | 0.80 |
| SVMC | 0.80 |


### Observations
After achieving the goal, I want to share some observations on this demo dataset.

1. About the next potential tokens:  
All Defi projects on BSC have higher returns. This result may have a bias as the period of the data collection is within this year. These BSC projects start late so that most of the increase is within this year.  
TVL indicates the quality of the projects. The higher quality of the project, the more people are willing to deposit the money in this project. Mkt_Cap represents the market capitalization of the token. The figure below displays the ratio of Mkt_Cap to TVL. The token could be underestimated if this ratio is smaller. Based on this observation, I notice that CRV and MDX are two tokens that are highly underestimated by the market. They could be the next potential tokens to the moon (not financial advice). Note that underestimation doesn't mean that the price will rapidly increase in a short period. Other reasons may affect the price as well. For example, both the above-mentioned tokens have low Cir_Ratio, which means that they have large pre-minted tokens. A larger supply may suppress the price longer.
![image](https://github.com/junzhuang-code/potential_defi_tokens/blob/main/images/mc_tvl.png)

2. About the top projects:  

| Name | TVL | Mkt_Cap |
| :-----: | :----: | :----: |
| Uniswap | 8.83 | 19.88 |
| PancakeSwap | 8.35 | 5.26 |
| Aave | 7.41 | 4.96 |
| Maker | 9.75 | 4.16 |
| Compound | 8.89 | 3.32 |

The table above presents the top five projects w.r.t. TVL and Mkt_Cap. The market has a high agreement on the top five projects. Within these projects, Compound has the lowest Return. One potential reason is that it has the lowest MC/TVL.  

3. About the categories:  

| Category | TVL | Mkt_Cap | Earning_Level |
| :-----: | :----: | :----: | :----: |
| Lending | 7.71 | 3.28 | 2.25 |
| Payments | 1.52 | 1.90 | 2.00 |
| Yield | 1.99 | 0.23 | 2.00 |
| Dexes | 5.09 | 4.10 | 1.85 |
| Derivatives | 0.77 | 0.84 | 1.00 |

The table above describes the average values of TVL, Mkt_Cap, and Earning_Level for each category. I notice that Lending projects have the highest earning level (2.25) and TVL (7.71) on average, whereas Dexes projects have the highest market capital (4.10) on average. Those two categories are very popular in this bull market.  

4. About the correlation:  
The heatmap presents the correlation among features. I'm interested in some features that are helpful to the investment as follows. Cir_Ratio and Price have a higher positive correlation as shorter supply may be easier to cause the increase of the price. A similar positive correlation is also applied to TVL and Mkt_Cap as higher quality projects can attract more investors. It's expected that Cir_Ratio has a higher positive correlation to the Return but actually, it is only 0.103821.  ![image](https://github.com/junzhuang-code/potential_defi_tokens/blob/main/images/corr.png)


### Conclusion
In this demo, I design a scheme to find out the next potential Defi token to the moon by machine learning approach. I collect some demo data from several famous cryptocurrency websites and build machine learning models to classify which token has higher potential. Besides, I also share some observations based on the demo data. In brief, MC/TVL is a helpful feature to find out which token is underestimated. Lending and Dexes projects have higher TVL and Mkt_Cap.  
In the future, this scheme could be extended to an online data analysis framework. More specially, we could monitor the data from the cryptocurrency websites' API and then analyze the data on-the-fly. To achieve the same goal, we could also convert the problem into a prediction task by using the Return as the label (we don't know the price in the future). Those attempts may be left for future work.
