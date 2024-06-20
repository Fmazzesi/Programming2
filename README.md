# Example of using the Zefix Advanced Tool

## Introduction

The Python package developed is designed to interact with the Swiss Official Gazette of Commerce (Zefix) API to retrieve detailed information about companies, including their acquisitions and organizational details. This package could be useful for financial analysts, market researchers, business consultants, and anyone interested in Swiss company data. It's entirely built to work with the Zefix API https://www.zefix.ch/en/search/entity/welcome.

The following documentation provides a comprehensive guide on how to install and use this package. It also explains what the functions do and their components.

Each function differs from the standard GET requests that you would normally use. See the description of each function to see its enhanced capabilities.

# Function #1 - search_companies_named

The search_companies_named function is useful for identifying companies that match a specific name or partial name, providing comprehensive information about each matching company.

This function takes in a company name or part of it (string) and returns a dataframe with information about all companies named like that. 

**Enhancement**

- automatically translates the status and purpose fields from german, french and italian to english. 
- searches multiple companies at once that share a certain name (e.g. 'UBS')
- directly provides understandable information about each company's legal form. Normally, you would only get a code that you need to then look up from another endpoint of the API. 
- automatically counts the number of publications on that firm, the number of firms directly taken over by that company, the number of branch offices and the number of old names of the company.
- allows you to save results in a json file
- returns the companies as a pandas dataframe or as a list of dictionaries

**Parameters:**

- *name (str):* name of the company (or part of it) to search for. Not caps sensitive.

- *simple (bool):* False by default. If True, returns a simplified version of the dictionary with only the name, ehraid, and legalSeat of the company.

- *save (bool):* False by default. If True, saves the data to a JSON file called "name_companies.json". If simple is also True at the same time, saves the data to a JSON file called "name_companies_simple.json" instead.

- *df (bool):* True by default. If True, returns the data as a pandas DataFrame. If False, returns the data as a list of dictionaries.

**Returns:**
    
- if df=False, it returns: 
    
list_of_companies (list): a list of dictionaries, each containing information about a company found in the search

- if df=True (default), it returns:

list_of_companies (DataFrame): a pandas DataFrame containing information about all companies found in the search

The dataframe in the list will contain the following information about the company:

- 'name':                 name of the company
- 'ehraid':               unique identifier of the company
- 'legalSeat':            location of the company's legal seat
- 'status':               status of the company (active or not)
- 'deleteDate':           date when the company was deleted (if applicable)
- 'wasTakenOverBy':       name of the company that took over this one (if applicable)
- 'purpose':              purpose of the company
- 'legalForm':            legal form of the company
- 'cancelled':            boolean value indicating if the company is cancelled or not
- 'n_of_shabPub':         counts the number of publications in the Swiss Official Gazette of Commerce
- 'n_of_branchOffices':   counts the number of branch offices of the company
- 'n_of_oldNames':        counts the number of old names of the company
- 'n_of_hasTakenOver':    counts the number of companies taken over by this one
- 'town':                 name of the town where the company is located
- 'swissZipCode':         Swiss zip code of the company

if simple=True, the dataframe/list of dictionaries will only contain the following:

- 'name':                name of the company
- 'ehraid':              unique identifier of the company
- 'legalSeat':           location of the company's legal seat

**Example**

options activated: simple, save and df.


```python
# Search Companies Named "Coop"
coop_simple_save_df = search_companies_named("Coop", simple=True, save=True, df=True)

# Display the DataFrame result
coop_simple_save_df

```

    Data saved to Coop_companies_simple.json





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>ehraid</th>
      <th>legalSeat</th>
      <th>cantonalExcerptWeb</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Baugenossenschaft Bel Air</td>
      <td>38828</td>
      <td>Evilard</td>
      <td>https://be.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Branchen Versicherung Genossenschaft</td>
      <td>323190</td>
      <td>Zürich</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Coopar Società Cooperativa in liquidazione</td>
      <td>1215435</td>
      <td>Lugano</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>COOPELIA, coopérative sociale pour l'encourage...</td>
      <td>364304</td>
      <td>Gland</td>
      <td>https://prestations.vd.ch/pub/101266/extract?l...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CoOpera Beteiligungen AG</td>
      <td>233739</td>
      <td>Bern</td>
      <td>https://be.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>CoOpera Immobilien AG</td>
      <td>418805</td>
      <td>Bern</td>
      <td>https://be.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Coopera International Sàrl</td>
      <td>1613929</td>
      <td>Lancy</td>
      <td>http://app2.ge.ch/ecohrcinternet/extract?lang=...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CoOpera Leasing AG</td>
      <td>130215</td>
      <td>Baar</td>
      <td>https://zg.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>CoOpera Sammelstiftung PUK</td>
      <td>280185</td>
      <td>Bern</td>
      <td>https://be.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>coOPERATION-zanotti GmbH</td>
      <td>1332539</td>
      <td>Beromünster</td>
      <td>https://lu.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Cooperativa abitativa VIV INSEMA</td>
      <td>1116969</td>
      <td>Terre di Pedemonte</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Cooperativa alambicco Mezzovico-Vira</td>
      <td>38801</td>
      <td>Mezzovico-Vira</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Cooperativa Albergo Olivone &amp; Posta</td>
      <td>1214085</td>
      <td>Blenio</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Cooperativa Assicurazione Bestiame Bovino del ...</td>
      <td>738220</td>
      <td>San Vittore</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Cooperativa BAOBAB</td>
      <td>1242335</td>
      <td>Bellinzona</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Cooperativa Bordo</td>
      <td>46649</td>
      <td>Bern</td>
      <td>https://be.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Cooperativa Camana</td>
      <td>30070</td>
      <td>Brusino Arsizio</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Cooperativa casa d'appartamenti OF (OFAHG)</td>
      <td>38818</td>
      <td>Massagno</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Cooperativa Case al Ponte</td>
      <td>38819</td>
      <td>Ascona</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Cooperativa chüra e vita a Zernez</td>
      <td>1152435</td>
      <td>Zernez</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Cooperativa Condominio Chesa Surlej</td>
      <td>61183</td>
      <td>Lugano</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Cooperativa "Corte del Duca"</td>
      <td>792072</td>
      <td>Monteceneri</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Cooperativa di Costruzione Domus</td>
      <td>38923</td>
      <td>Chiasso</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Cooperativa di Costruzione FERCASA</td>
      <td>231093</td>
      <td>Novazzano</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>COOPERATIVA DI COSTRUZIONI "LA MODERNA"</td>
      <td>243358</td>
      <td>Bellinzona</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Cooperativa di costruzioni Mota Farun</td>
      <td>1051371</td>
      <td>Bregaglia</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Cooperativa di Landaviva di Landarenca</td>
      <td>834997</td>
      <td>Calanca</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Cooperativa Ecohabitat</td>
      <td>311214</td>
      <td>Locarno</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Cooperativa Edilizia CEM in liquidazione</td>
      <td>246863</td>
      <td>Mendrisio</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Cooperativa Elettrica di Faido (CEF)</td>
      <td>61186</td>
      <td>Faido</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Cooperativa Essiccazione Tabacco, CETA</td>
      <td>253272</td>
      <td>Cadenazzo</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>31</th>
      <td>COOPERATIVA IMMOBILIARE SVIZZERA 2011</td>
      <td>1022526</td>
      <td>Lugano</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Cooperativa La Cascata</td>
      <td>31596</td>
      <td>Rossa</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Cooperativa Lavoratori Indipendenti Bricolle</td>
      <td>258682</td>
      <td>Locarno</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Cooperativa Librerie Alternative in liquidazione</td>
      <td>220690</td>
      <td>Locarno</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Cooperativa Macchine Agricole di Breno-Fescogg...</td>
      <td>61187</td>
      <td>Alto Malcantone</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Cooperativa Macello Regionale Avegno</td>
      <td>874485</td>
      <td>Avegno Gordevio</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Cooperativa Popolare Società Cooperativa</td>
      <td>65111</td>
      <td>Balerna</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Cooperativa SALEGGIO, costruzioni di alloggi</td>
      <td>246499</td>
      <td>Locarno</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Cooperativa sociale Maggia</td>
      <td>82919</td>
      <td>Maggia</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Cooperativa Stizun Ruschein</td>
      <td>885497</td>
      <td>Ilanz/Glion</td>
      <td>https://gr.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Cooperativa Taxi Muralto</td>
      <td>1356860</td>
      <td>Muralto</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Cooperativa Tempo libero dei lavoratori</td>
      <td>246612</td>
      <td>Balerna</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Cooperativa Tennis Caslano in liquidazione</td>
      <td>350385</td>
      <td>Caslano</td>
      <td>https://ti.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Coopérative agricole de la Ferme du Quartier d...</td>
      <td>1403251</td>
      <td>Meyrin</td>
      <td>http://app2.ge.ch/ecohrcinternet/extract?lang=...</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Coopérative agricole d'utilisation de machines...</td>
      <td>1247317</td>
      <td>Ponthaux</td>
      <td>https://adm.appls.fr.ch/hrcmatic/extract?compa...</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Coopérative agricole d'utilisation de machines...</td>
      <td>305057</td>
      <td>Missy</td>
      <td>https://prestations.vd.ch/pub/101266/extract?l...</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Coopérative agricole d'utilisation de machines...</td>
      <td>811994</td>
      <td>Lignerolle</td>
      <td>https://prestations.vd.ch/pub/101266/extract?l...</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Coopérative Alliance-CH</td>
      <td>775560</td>
      <td>La Tène</td>
      <td>https://hrc.ne.ch/hrcintapp/externalCompanyRep...</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Coopérative Aquacasa</td>
      <td>67497</td>
      <td>Haute-Ajoie</td>
      <td>https://ju.chregister.ch/cr-portal/auszug/ausz...</td>
    </tr>
  </tbody>
</table>
</div>



# FUNCTION #2 - get_acquisitions_data

The get_acquisitions_data function is essential for tracking the acquisition history of a specific company, including both direct and indirect acquisitions. This is especially useful, since it automates the lengthy task of looking up each individual company that was acquired to see if they also acquired other companies (and so on). For example, with a big firm of the likes of UBS, without this function you would have to look up about *one hundred* different companies to understand how far the tree of minor and major acquisitions extends.

For example, if firm A has taken over firm B, and firm B has taken over firm C, the function will return information about firm A, firm B, and firm C. Starting from A, the function will count the number of "hops" to reach the last firm in the chain. The function has also an option to save the data to a JSON file, and you can ask to return the information either as a pandas dataframe or as a list of dictionaries. The latter can be used to visualize the tree of companies using the plot_acquisitions function, explained later. 
    
**Parameters:**

- *ehraid (str):* ehraid of the firm to start from
- *hops (int):* DO NOT CHANGE THIS VALUE, it is used as a counter for the number of hops from the initial ehraid
- *save (bool):* if True, saves the data to a JSON file called 'takeovers.json'
- *df (bool):* if True, returns the data as a pandas DataFrame

**Returns:**

- if df=False (default): 

acquisitions (list): a list of dictionaries, each containing information about a firm and the firms it has taken over

- if df=True:

acquisitions (DataFrame): a pandas DataFrame containing information about all firms and the firms they have taken over

**Example**

All acquisitions of UBS AG (ehraid is 415520). Save option is activated, df option is not.


```python
# Example: Get Acquisitions Data for Company with ehraid 415520, which is UBS AG ERHAID
ubs_ag_acquisitions = get_acquisitions_data(415520, hops=0, save=True, df=False)

# Display the result
ubs_ag_acquisitions
```

    Data saved to takeovers.json





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>ehraid</th>
      <th>legalSeat</th>
      <th>legalFormId</th>
      <th>status</th>
      <th>cantonalExcerptWeb</th>
      <th>deleteDate</th>
      <th>hops</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>UBS AG</td>
      <td>415520</td>
      <td>Basel</td>
      <td>3</td>
      <td>Active</td>
      <td>https://bs.chregister.ch/cr-portal/auszug/ausz...</td>
      <td>None</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Credit Suisse AG</td>
      <td>388851</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2024-06-04</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABZ - Finanz- und Beteiligungsgesellschaft AG</td>
      <td>619</td>
      <td>Zug</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zg.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2009-07-06</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Faminta AG</td>
      <td>55686</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2008-04-04</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hochhaus zur Palme AG</td>
      <td>81396</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2006-07-06</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Stadion Zürich AG</td>
      <td>77348</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2010-07-12</td>
      <td>2</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Credit Suisse (International) Holding AG</td>
      <td>390377</td>
      <td>Zug</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zg.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2010-07-06</td>
      <td>2</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Credit Suisse First Boston Management AG</td>
      <td>399185</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2006-07-06</td>
      <td>3</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Credit Suisse First Boston Services AG</td>
      <td>399275</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2006-07-06</td>
      <td>3</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Aktiengesellschaft Bellevue</td>
      <td>17116</td>
      <td>Zürich</td>
      <td>3</td>
      <td>Deleted</td>
      <td>https://zh.chregister.ch/cr-portal/auszug/zefi...</td>
      <td>2010-12-15</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>104 rows × 8 columns</p>
</div>



# FUNCTION #3 - plot_acquisitions

The plot_acquisitions function offers a visual representation of a company's acquisition chain, illustrating the number of acquisition "hops" from the initial company. 

Takes in the output of the function **acquisitions_data** with the option df=False: a list of dictionaries with information about firms and their acquisitions. Plots the acquisitions on a graph.

From left to right, the x axis represents the number of acquisition "hops" from the initial firm, which has hops=0. 
    
**Parameters:**

- *acquisitions (list of dictionaries):* list of dictionaries with information about firms and their acquisitions. You can get data structured this way running the function acquisitions_data from the same package as this one.
    
**Returns:** 

- A plot displaying the acquisition chains, with the x-axis representing the number of hops.

**Example**

We are using the output of the get_acquisitions_data example from before, concerning UBS AG.


```python
# Example: Plot Acquisitions Data
plot_acquisitions(ubs_ag_acquisitions_no_save_no_dataframe)
```


    
![Immagine grafico esempio](https://github.com/Fmazzesi/Zefix-Tools/assets/161603011/73e5e54f-568b-4531-9563-f5818f15327f)

    


### ⚠️ Warning
You need to input a list of dictionaries that you obtained from the function get_acquisition_data with the option df = False. 
Otherwise, you will get an error code like in the following example.


```python
plot_acquisitions(ubs_ag_acquisitions)
```




    'Please provide a list of dictionaries with information about firms and their acquisitions as input. You can get this data by running the function acquisitions_data in this same package. Use the default option df=False'



# FUNTION #4 - check_acquirers

The check_acquirers function provides detailed information about companies that have taken over a specific firm, identified by its EHRAID (a unique identifier assigned to companies in the Swiss Official Gazette of Commerce).

It finds all acquirers of a certain company in one go, automatically implementing translations of the status and purpose of that company from french, german or italian to english. It also automatically retrieves an understandable company's legal form from another zefix endpoint, instead of just giving its ID as output. The output can be a pandas dataframe or a list of dictionaries.


**Parameters:**

- *ehraid (str):* The unique identifier (EHRAID) of the company whose acquirers need to be checked. This must be a string representing the EHRAID of the target company.
- *df (bool):* Default is True. If True, the function returns the data as a pandas DataFrame. If False, the data is returned as a list of dictionaries.

**Returns:**

- If df is True: 

Returns a pandas DataFrame containing detailed information about the companies that have taken over the specified company.

- If df is False: 

Returns a list of dictionaries with detailed information about the acquirers.

The resulting DataFrame or list includes the following information about each acquirer:

- 'name:' The name of the acquirer company.
- 'ehraid:'                   The unique identifier of the acquirer company.
- 'legalSeat:'                The location of the acquirer's legal seat.
- 'legalFormId:'              The legal form of the acquirer company.
- 'status:'                   The current status of the acquirer company (translated into English if necessary).
- 'cantonalExcerptWeb:'       A web link to the cantonal excerpt for the acquirer company.
- 'deleteDate:'               The date when the acquirer company was deleted, if applicable.
- 'purpose:'                  The purpose of the acquirer company, translated into English.
- 'capitalNominal:'           The nominal capital of the acquirer company.

**Example**

Example with the option dataframe active for the company Virex SA with (its ehraid is 247693)


```python
acquirers_df = check_acquirers("247693", df=True)

acquirers_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>ehraid</th>
      <th>legalSeat</th>
      <th>legalFormId</th>
      <th>status</th>
      <th>cantonalExcerptWeb</th>
      <th>deleteDate</th>
      <th>purpose</th>
      <th>capitalNominal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ROLEX SA</td>
      <td>122015</td>
      <td>Genève</td>
      <td>Corporation</td>
      <td>Active</td>
      <td>http://app2.ge.ch/ecohrcinternet/extract?lang=...</td>
      <td>None</td>
      <td>The manufacture and trade of watches, time mea...</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>


