# Downloading the historical data for NSE futures stocks

The stocks symbols of NSE futures stocks are read from local .csv file. The code downloads the data in '1m', '5m' and '1d' time frame in steps. It was observed that code gives error when large amount of data is downloaded. It takes huge time and code gives timeouterror. Hence, the data is downloaded in months wise.


```python
import finmetry as fm
import pandas as pd
import numpy as np
import datetime as dtm
import os

# market_data_foldpath = r"X:\finmetry"
```

## Logging into Client5paisa


```python
### initializing scrip_master
scrip_master_filepath = os.path.join(market_data_foldpath, "scrip_master.csv")
# scrip_master = fm.client_5paisa.ScripMaster()
# scrip_master.save(scrip_master_filepath)
scrip_master = fm.client_5paisa.ScripMaster(filepath=scrip_master_filepath)
### logging in
c_5p = fm.client_5paisa.Client5paisa(
    email=email, password=password, dob=dob, cred=cred, scrip_master=scrip_master
)
```

     18:42:36 | Logged in!!
    

---
---
### Loading NSE futures stocklist

Reading the Symbols from `all_nse.csv` file from which the list of `Stock` class will be generated.


```python
symbols = pd.read_csv("all_nse.csv")["symbol"].to_list()
sl1 = []
for sym in symbols:
    s1 = fm.Stock(
        symbol=sym.upper(),
        exchange="N",
        exchange_type="C",
        store_local=True,
        local_data_foldpath=market_data_foldpath,
    )
    sl1.append(s1)
sm1 = scrip_master.get_scrip(sl1)
```

The start and end date for all the data downloading.


```python
start = dtm.datetime(2023, 4, 15)
end = dtm.datetime(2023, 8, 1)
```

## Downloading 1min data

Here, the timeinterval between start and end date is kept as 30 days.


```python
dt1 = start
while dt1 <= end:
    start_date = dt1
    end_date = dt1 + dtm.timedelta(days=30)
    for s1 in sl1:
        n_try = 0
        while n_try < 20:
            try:
                c_5p.download_historical_data(stocklist=[s1], interval="1m", start=start_date, end=end_date)
                break
            except KeyboardInterrupt:
                raise KeyboardInterrupt
            except:
                n_try += 1
                print(n_try)
    dt1 = end_date
```

    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202305_1m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202305_1m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202305_1m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202305_1m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202305_1m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202305_1m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202305_1m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202305_1m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202305_1m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202305_1m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202305_1m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202305_1m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202305_1m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202305_1m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202305_1m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202305_1m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202305_1m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202305_1m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202305_1m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202305_1m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202305_1m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202305_1m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202305_1m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202305_1m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202305_1m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202305_1m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202305_1m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202305_1m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202305_1m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202305_1m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202305_1m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202305_1m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202305_1m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202305_1m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202305_1m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202305_1m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202305_1m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202305_1m.pickle
    HDFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202305_1m.pickle
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202305_1m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202305_1m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202305_1m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202305_1m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202305_1m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202305_1m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202305_1m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202305_1m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202305_1m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202305_1m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202305_1m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202305_1m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202305_1m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202305_1m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202305_1m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202305_1m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202305_1m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202305_1m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202305_1m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202305_1m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202305_1m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202305_1m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202305_1m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202305_1m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202305_1m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202305_1m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202305_1m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202305_1m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202305_1m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202305_1m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202305_1m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202305_1m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202305_1m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202305_1m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202305_1m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202305_1m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202305_1m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202305_1m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202305_1m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202305_1m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202305_1m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202305_1m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202305_1m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202305_1m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202305_1m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202305_1m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202305_1m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202305_1m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202305_1m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202305_1m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202305_1m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202305_1m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202305_1m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202305_1m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202305_1m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202305_1m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202305_1m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202305_1m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202305_1m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202305_1m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202305_1m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202305_1m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202305_1m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202305_1m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202305_1m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202305_1m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202305_1m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202305_1m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202305_1m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202305_1m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202305_1m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202305_1m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202305_1m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202305_1m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202305_1m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202305_1m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202305_1m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202305_1m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202305_1m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202305_1m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202305_1m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202305_1m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202305_1m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202305_1m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202305_1m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202305_1m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202305_1m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202305_1m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202305_1m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202305_1m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202305_1m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202305_1m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202305_1m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202305_1m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202305_1m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202305_1m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202305_1m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202305_1m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202305_1m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202305_1m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202305_1m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202305_1m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202305_1m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202305_1m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202305_1m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202305_1m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202305_1m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202305_1m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202305_1m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202305_1m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202305_1m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202305_1m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202305_1m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202305_1m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202305_1m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202305_1m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202305_1m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202305_1m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202305_1m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202305_1m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202305_1m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202305_1m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202305_1m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202305_1m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202305_1m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202305_1m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202305_1m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202305_1m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202305_1m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202305_1m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202305_1m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202305_1m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202305_1m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202305_1m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202305_1m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202305_1m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202305_1m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202305_1m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202305_1m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202305_1m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202305_1m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202305_1m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202305_1m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202305_1m.pickle
    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202306_1m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202306_1m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202306_1m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202306_1m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202306_1m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202306_1m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202306_1m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202306_1m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202306_1m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202306_1m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202306_1m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202306_1m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202306_1m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202306_1m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202306_1m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202306_1m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202306_1m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202306_1m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202306_1m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202306_1m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202306_1m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202306_1m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202306_1m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202306_1m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202306_1m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202306_1m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202306_1m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202306_1m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202306_1m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202306_1m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202306_1m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202306_1m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202306_1m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202306_1m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202306_1m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202306_1m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202306_1m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202306_1m.pickle
    HDFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202306_1m.pickle
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202306_1m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202306_1m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202306_1m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202306_1m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202306_1m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202306_1m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202306_1m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202306_1m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202306_1m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202306_1m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202306_1m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202306_1m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202306_1m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202306_1m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202306_1m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202306_1m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202306_1m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202306_1m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202306_1m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202306_1m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202306_1m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202306_1m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202306_1m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202306_1m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202306_1m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202306_1m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202306_1m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202306_1m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202306_1m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202306_1m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202306_1m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202306_1m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202306_1m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202306_1m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202306_1m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202306_1m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202306_1m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202306_1m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202306_1m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202306_1m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202306_1m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202306_1m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202306_1m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202306_1m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202306_1m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202306_1m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202306_1m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202306_1m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202306_1m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202306_1m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202306_1m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202306_1m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202306_1m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202306_1m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202306_1m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202306_1m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202306_1m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202306_1m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202306_1m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202306_1m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202306_1m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202306_1m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202306_1m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202306_1m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202306_1m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202306_1m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202306_1m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202306_1m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202306_1m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202306_1m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202306_1m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202306_1m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202306_1m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202306_1m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202306_1m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202306_1m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202306_1m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202306_1m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202306_1m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202306_1m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202306_1m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202306_1m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202306_1m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202306_1m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202306_1m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202306_1m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202306_1m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202306_1m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202306_1m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202306_1m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202306_1m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202306_1m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202306_1m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202306_1m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202306_1m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202306_1m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202306_1m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202306_1m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202306_1m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202306_1m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202306_1m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202306_1m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202306_1m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202306_1m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202306_1m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202306_1m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202306_1m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202306_1m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202306_1m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202306_1m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202306_1m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202306_1m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202306_1m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202306_1m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202306_1m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202306_1m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202306_1m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202306_1m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202306_1m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202306_1m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202306_1m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202306_1m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202306_1m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202306_1m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202306_1m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202306_1m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202306_1m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202306_1m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202306_1m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202306_1m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202306_1m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202306_1m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202306_1m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202306_1m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202306_1m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202306_1m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202306_1m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202306_1m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202306_1m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202306_1m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202306_1m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202306_1m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202306_1m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202306_1m.pickle
    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202307_1m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202307_1m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202307_1m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202307_1m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202307_1m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202307_1m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202307_1m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202307_1m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202307_1m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202307_1m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202307_1m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202307_1m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202307_1m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202307_1m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202307_1m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202307_1m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202307_1m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202307_1m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202307_1m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202307_1m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202307_1m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202307_1m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202307_1m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202307_1m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202307_1m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202307_1m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202307_1m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202307_1m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202307_1m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202307_1m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202307_1m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202307_1m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202307_1m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202307_1m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202307_1m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202307_1m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202307_1m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202307_1m.pickle
    HDFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202307_1m.pickle
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202307_1m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202307_1m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202307_1m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202307_1m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202307_1m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202307_1m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202307_1m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202307_1m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202307_1m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202307_1m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202307_1m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202307_1m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202307_1m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202307_1m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202307_1m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202307_1m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202307_1m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202307_1m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202307_1m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202307_1m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202307_1m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202307_1m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202307_1m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202307_1m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202307_1m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202307_1m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202307_1m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202307_1m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202307_1m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202307_1m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202307_1m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202307_1m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202307_1m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202307_1m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202307_1m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202307_1m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202307_1m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202307_1m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202307_1m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202307_1m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202307_1m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202307_1m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202307_1m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202307_1m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202307_1m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202307_1m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202307_1m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202307_1m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202307_1m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202307_1m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202307_1m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202307_1m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202307_1m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202307_1m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202307_1m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202307_1m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202307_1m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202307_1m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202307_1m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202307_1m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202307_1m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202307_1m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202307_1m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202307_1m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202307_1m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202307_1m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202307_1m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202307_1m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202307_1m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202307_1m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202307_1m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202307_1m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202307_1m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202307_1m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202307_1m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202307_1m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202307_1m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202307_1m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202307_1m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202307_1m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202307_1m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202307_1m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202307_1m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202307_1m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202307_1m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202307_1m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202307_1m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202307_1m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202307_1m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202307_1m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202307_1m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202307_1m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202307_1m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202307_1m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202307_1m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202307_1m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202307_1m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202307_1m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202307_1m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202307_1m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202307_1m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202307_1m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202307_1m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202307_1m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202307_1m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202307_1m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202307_1m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202307_1m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202307_1m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202307_1m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202307_1m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202307_1m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202307_1m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202307_1m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202307_1m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202307_1m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202307_1m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202307_1m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202307_1m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202307_1m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202307_1m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202307_1m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202307_1m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202307_1m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202307_1m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202307_1m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202307_1m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202307_1m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202307_1m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202307_1m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202307_1m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202307_1m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202307_1m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202307_1m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202307_1m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202307_1m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202307_1m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202307_1m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202307_1m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202307_1m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202307_1m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202307_1m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202307_1m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202307_1m.pickle
    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202308_1m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202308_1m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202308_1m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202308_1m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202308_1m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202308_1m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202308_1m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202308_1m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202308_1m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202308_1m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202308_1m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202308_1m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202308_1m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202308_1m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202308_1m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202308_1m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202308_1m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202308_1m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202308_1m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202308_1m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202308_1m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202308_1m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202308_1m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202308_1m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202308_1m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202308_1m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202308_1m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202308_1m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202308_1m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202308_1m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202308_1m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202308_1m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202308_1m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202308_1m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202308_1m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202308_1m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202308_1m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202308_1m.pickle
    HDFC
    1
    HDFC
    2
    HDFC
    3
    HDFC
    4
    HDFC
    5
    HDFC
    6
    HDFC
    7
    HDFC
    8
    HDFC
    9
    HDFC
    10
    HDFC
    11
    HDFC
    12
    HDFC
    13
    HDFC
    14
    HDFC
    15
    HDFC
    16
    HDFC
    17
    HDFC
    18
    HDFC
    19
    HDFC
    20
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202308_1m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202308_1m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202308_1m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202308_1m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202308_1m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202308_1m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202308_1m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202308_1m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202308_1m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202308_1m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202308_1m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202308_1m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202308_1m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202308_1m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202308_1m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202308_1m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202308_1m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202308_1m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202308_1m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202308_1m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202308_1m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202308_1m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202308_1m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202308_1m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202308_1m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202308_1m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202308_1m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202308_1m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202308_1m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202308_1m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202308_1m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202308_1m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202308_1m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202308_1m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202308_1m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202308_1m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202308_1m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202308_1m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202308_1m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202308_1m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202308_1m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202308_1m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202308_1m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202308_1m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202308_1m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202308_1m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202308_1m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202308_1m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202308_1m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202308_1m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202308_1m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202308_1m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202308_1m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202308_1m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202308_1m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202308_1m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202308_1m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202308_1m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202308_1m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202308_1m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202308_1m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202308_1m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202308_1m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202308_1m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202308_1m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202308_1m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202308_1m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202308_1m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202308_1m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202308_1m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202308_1m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202308_1m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202308_1m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202308_1m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202308_1m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202308_1m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202308_1m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202308_1m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202308_1m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202308_1m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202308_1m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202308_1m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202308_1m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202308_1m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202308_1m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202308_1m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202308_1m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202308_1m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202308_1m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202308_1m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202308_1m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202308_1m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202308_1m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202308_1m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202308_1m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202308_1m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202308_1m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202308_1m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202308_1m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202308_1m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202308_1m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202308_1m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202308_1m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202308_1m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202308_1m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202308_1m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202308_1m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202308_1m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202308_1m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202308_1m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202308_1m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202308_1m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202308_1m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202308_1m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202308_1m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202308_1m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202308_1m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202308_1m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202308_1m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202308_1m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202308_1m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202308_1m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202308_1m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202308_1m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202308_1m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202308_1m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202308_1m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202308_1m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202308_1m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202308_1m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202308_1m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202308_1m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202308_1m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202308_1m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202308_1m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202308_1m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202308_1m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202308_1m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202308_1m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202308_1m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202308_1m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202308_1m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202308_1m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202308_1m.pickle
    

## Downloading 5min data

Here, the timeinterval between start and end date is kept as 90 days.


```python
dt1 = start
while dt1 <= end:
    start_date = dt1
    end_date = dt1 + dtm.timedelta(days=90)
    for s1 in sl1:
        n_try = 0
        while n_try < 20:
            try:
                c_5p.download_historical_data(stocklist=[s1], interval="5m", start=start_date, end=end_date)
                break
            except KeyboardInterrupt:
                raise KeyboardInterrupt
            except:
                n_try += 1
                print(n_try)
    dt1 = end_date
```

    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202307_5m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202307_5m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202307_5m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202307_5m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202307_5m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202307_5m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202307_5m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202307_5m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202307_5m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202307_5m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202307_5m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202307_5m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202307_5m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202307_5m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202307_5m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202307_5m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202307_5m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202307_5m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202307_5m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202307_5m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202307_5m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202307_5m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202307_5m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202307_5m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202307_5m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202307_5m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202307_5m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202307_5m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202307_5m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202307_5m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202307_5m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202307_5m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202307_5m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202307_5m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202307_5m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202307_5m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202307_5m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202307_5m.pickle
    HDFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202307_5m.pickle
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202307_5m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202307_5m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202307_5m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202307_5m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202307_5m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202307_5m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202307_5m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202307_5m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202307_5m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202307_5m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202307_5m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202307_5m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202307_5m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202307_5m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202307_5m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202307_5m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202307_5m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202307_5m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202307_5m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202307_5m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202307_5m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202307_5m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202307_5m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202307_5m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202307_5m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202307_5m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202307_5m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202307_5m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202307_5m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202307_5m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202307_5m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202307_5m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202307_5m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202307_5m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202307_5m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202307_5m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202307_5m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202307_5m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202307_5m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202307_5m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202307_5m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202307_5m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202307_5m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202307_5m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202307_5m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202307_5m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202307_5m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202307_5m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202307_5m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202307_5m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202307_5m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202307_5m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202307_5m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202307_5m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202307_5m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202307_5m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202307_5m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202307_5m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202307_5m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202307_5m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202307_5m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202307_5m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202307_5m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202307_5m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202307_5m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202307_5m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202307_5m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202307_5m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202307_5m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202307_5m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202307_5m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202307_5m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202307_5m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202307_5m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202307_5m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202307_5m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202307_5m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202307_5m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202307_5m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202307_5m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202307_5m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202307_5m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202307_5m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202307_5m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202307_5m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202307_5m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202307_5m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202307_5m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202307_5m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202307_5m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202307_5m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202307_5m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202307_5m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202307_5m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202307_5m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202307_5m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202307_5m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202307_5m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202307_5m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202307_5m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202307_5m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202307_5m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202307_5m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202307_5m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202307_5m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202307_5m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202307_5m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202307_5m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202307_5m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202307_5m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202307_5m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202307_5m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202307_5m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202307_5m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202307_5m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202307_5m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202307_5m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202307_5m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202307_5m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202307_5m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202307_5m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202307_5m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202307_5m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202307_5m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202307_5m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202307_5m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202307_5m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202307_5m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202307_5m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202307_5m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202307_5m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202307_5m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202307_5m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202307_5m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202307_5m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202307_5m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202307_5m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202307_5m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202307_5m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202307_5m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202307_5m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202307_5m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202307_5m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202307_5m.pickle
    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202308_5m.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202308_5m.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202308_5m.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202308_5m.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202308_5m.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202308_5m.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202308_5m.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202308_5m.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202308_5m.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202308_5m.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202308_5m.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202308_5m.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202308_5m.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202308_5m.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202308_5m.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202308_5m.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202308_5m.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202308_5m.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202308_5m.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202308_5m.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202308_5m.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202308_5m.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202308_5m.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202308_5m.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202308_5m.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202308_5m.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202308_5m.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202308_5m.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202308_5m.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202308_5m.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202308_5m.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202308_5m.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202308_5m.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202308_5m.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202308_5m.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202308_5m.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202308_5m.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202308_5m.pickle
    HDFC
    1
    HDFC
    2
    HDFC
    3
    HDFC
    4
    HDFC
    5
    HDFC
    6
    HDFC
    7
    HDFC
    8
    HDFC
    9
    HDFC
    10
    HDFC
    11
    HDFC
    12
    HDFC
    13
    HDFC
    14
    HDFC
    15
    HDFC
    16
    HDFC
    17
    HDFC
    18
    HDFC
    19
    HDFC
    20
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202308_5m.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202308_5m.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202308_5m.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202308_5m.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202308_5m.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202308_5m.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202308_5m.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202308_5m.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202308_5m.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202308_5m.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202308_5m.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202308_5m.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202308_5m.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202308_5m.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202308_5m.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202308_5m.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202308_5m.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202308_5m.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202308_5m.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202308_5m.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202308_5m.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202308_5m.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202308_5m.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202308_5m.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202308_5m.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202308_5m.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202308_5m.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202308_5m.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202308_5m.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202308_5m.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202308_5m.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202308_5m.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202308_5m.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202308_5m.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202308_5m.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202308_5m.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202308_5m.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202308_5m.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202308_5m.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202308_5m.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202308_5m.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202308_5m.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202308_5m.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202308_5m.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202308_5m.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202308_5m.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202308_5m.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202308_5m.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202308_5m.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202308_5m.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202308_5m.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202308_5m.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202308_5m.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202308_5m.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202308_5m.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202308_5m.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202308_5m.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202308_5m.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202308_5m.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202308_5m.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202308_5m.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202308_5m.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202308_5m.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202308_5m.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202308_5m.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202308_5m.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202308_5m.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202308_5m.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202308_5m.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202308_5m.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202308_5m.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202308_5m.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202308_5m.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202308_5m.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202308_5m.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202308_5m.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202308_5m.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202308_5m.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202308_5m.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202308_5m.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202308_5m.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202308_5m.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202308_5m.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202308_5m.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202308_5m.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202308_5m.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202308_5m.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202308_5m.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202308_5m.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202308_5m.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202308_5m.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202308_5m.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202308_5m.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202308_5m.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202308_5m.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202308_5m.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202308_5m.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202308_5m.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202308_5m.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202308_5m.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202308_5m.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202308_5m.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202308_5m.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202308_5m.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202308_5m.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202308_5m.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202308_5m.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202308_5m.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202308_5m.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202308_5m.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202308_5m.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202308_5m.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202308_5m.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202308_5m.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202308_5m.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202308_5m.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202308_5m.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202308_5m.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202308_5m.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202308_5m.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202308_5m.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202308_5m.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202308_5m.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202308_5m.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202308_5m.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202308_5m.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202308_5m.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202308_5m.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202308_5m.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202308_5m.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202308_5m.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202308_5m.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202308_5m.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202308_5m.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202308_5m.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202308_5m.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202308_5m.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202308_5m.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202308_5m.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202308_5m.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202308_5m.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202308_5m.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202308_5m.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202308_5m.pickle
    

## Downloading 1Day data

Here, data is downloaded in one go.


```python
for s1 in sl1:
    n_try = 0
    while n_try < 20:
        try:
            c_5p.download_historical_data(stocklist=[s1], interval="1d", start=start, end=end)
            break
        except KeyboardInterrupt:
            raise KeyboardInterrupt
        except:
            n_try += 1
            print(n_try)
```

    ESCORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ESCORTS\202308_1d.pickle
    CHAMBLFERT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHAMBLFERT\202308_1d.pickle
    PNB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PNB\202308_1d.pickle
    DALBHARAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DALBHARAT\202308_1d.pickle
    SBIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBIN\202308_1d.pickle
    SRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SRF\202308_1d.pickle
    PIDILITIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIDILITIND\202308_1d.pickle
    ABFRL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABFRL\202308_1d.pickle
    ASTRAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASTRAL\202308_1d.pickle
    GRANULES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRANULES\202308_1d.pickle
    IOC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IOC\202308_1d.pickle
    HDFCBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCBANK\202308_1d.pickle
    POWERGRID
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POWERGRID\202308_1d.pickle
    INDIACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIACEM\202308_1d.pickle
    PFIZER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFIZER\202308_1d.pickle
    VOLTAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VOLTAS\202308_1d.pickle
    RELIANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RELIANCE\202308_1d.pickle
    HINDUNILVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDUNILVR\202308_1d.pickle
    MFSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MFSL\202308_1d.pickle
    DIVISLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIVISLAB\202308_1d.pickle
    DABUR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DABUR\202308_1d.pickle
    ICICIBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIBANK\202308_1d.pickle
    HAVELLS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAVELLS\202308_1d.pickle
    DEEPAKNTR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DEEPAKNTR\202308_1d.pickle
    ABBOTINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ABBOTINDIA\202308_1d.pickle
    PIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PIIND\202308_1d.pickle
    CUB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUB\202308_1d.pickle
    LAURUSLABS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LAURUSLABS\202308_1d.pickle
    CANBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANBK\202308_1d.pickle
    COROMANDEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COROMANDEL\202308_1d.pickle
    IPCALAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IPCALAB\202308_1d.pickle
    SUNPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNPHARMA\202308_1d.pickle
    GODREJCP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJCP\202308_1d.pickle
    NESTLEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NESTLEIND\202308_1d.pickle
    ASIANPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASIANPAINT\202308_1d.pickle
    BALKRISIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BALKRISIND\202308_1d.pickle
    ALKEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ALKEM\202308_1d.pickle
    BERGEPAINT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BERGEPAINT\202308_1d.pickle
    HDFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFC\202307_1d.pickle
    SBILIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBILIFE\202308_1d.pickle
    COLPAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COLPAL\202308_1d.pickle
    POLYCAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_POLYCAB\202308_1d.pickle
    SYNGENE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SYNGENE\202308_1d.pickle
    ICICIPRULI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIPRULI\202308_1d.pickle
    PEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PEL\202308_1d.pickle
    EXIDEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EXIDEIND\202308_1d.pickle
    JKCEMENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JKCEMENT\202308_1d.pickle
    INFY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INFY\202308_1d.pickle
    ITC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ITC\202308_1d.pickle
    CUMMINSIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CUMMINSIND\202308_1d.pickle
    HINDPETRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDPETRO\202308_1d.pickle
    BHARTIARTL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARTIARTL\202308_1d.pickle
    DLF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DLF\202308_1d.pickle
    AXISBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AXISBANK\202308_1d.pickle
    IBULHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IBULHSGFIN\202308_1d.pickle
    IDEA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDEA\202308_1d.pickle
    TITAN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TITAN\202308_1d.pickle
    TATACONSUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACONSUM\202308_1d.pickle
    NAVINFLUOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAVINFLUOR\202308_1d.pickle
    BAJAJ-AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJ-AUTO\202308_1d.pickle
    NTPC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NTPC\202308_1d.pickle
    HDFCLIFE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCLIFE\202308_1d.pickle
    LICHSGFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LICHSGFIN\202308_1d.pickle
    CROMPTON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CROMPTON\202308_1d.pickle
    L&TFH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_L&TFH\202308_1d.pickle
    MCDOWELL-N
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCDOWELL-N\202308_1d.pickle
    ULTRACEMCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ULTRACEMCO\202308_1d.pickle
    BRITANNIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BRITANNIA\202308_1d.pickle
    LTTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LTTS\202308_1d.pickle
    ADANIENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIENT\202308_1d.pickle
    GRASIM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GRASIM\202308_1d.pickle
    IRCTC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IRCTC\202308_1d.pickle
    NAUKRI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAUKRI\202308_1d.pickle
    PAGEIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PAGEIND\202308_1d.pickle
    LUPIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LUPIN\202308_1d.pickle
    PETRONET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PETRONET\202308_1d.pickle
    BATAINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BATAINDIA\202308_1d.pickle
    ICICIGI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ICICIGI\202308_1d.pickle
    WHIRLPOOL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WHIRLPOOL\202308_1d.pickle
    KOTAKBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_KOTAKBANK\202308_1d.pickle
    GMRINFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GMRINFRA\202308_1d.pickle
    STAR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_STAR\202308_1d.pickle
    TCS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TCS\202308_1d.pickle
    CIPLA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CIPLA\202308_1d.pickle
    HINDALCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HINDALCO\202308_1d.pickle
    BSOFT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BSOFT\202308_1d.pickle
    CHOLAFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CHOLAFIN\202308_1d.pickle
    AARTIIND
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AARTIIND\202308_1d.pickle
    RECLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RECLTD\202308_1d.pickle
    ADANIPORTS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ADANIPORTS\202308_1d.pickle
    BANKBARODA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKBARODA\202308_1d.pickle
    UBL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UBL\202308_1d.pickle
    ACC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ACC\202308_1d.pickle
    IGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IGL\202308_1d.pickle
    DIXON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DIXON\202308_1d.pickle
    HDFCAMC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HDFCAMC\202308_1d.pickle
    JSWSTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JSWSTEEL\202308_1d.pickle
    TATACHEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATACHEM\202308_1d.pickle
    LALPATHLAB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LALPATHLAB\202308_1d.pickle
    NMDC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NMDC\202308_1d.pickle
    INDUSTOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSTOWER\202308_1d.pickle
    SIEMENS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SIEMENS\202308_1d.pickle
    PFC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PFC\202308_1d.pickle
    MARICO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARICO\202308_1d.pickle
    BAJAJFINSV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJAJFINSV\202308_1d.pickle
    BANDHANBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANDHANBNK\202308_1d.pickle
    M&MFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&MFIN\202308_1d.pickle
    RAMCOCEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RAMCOCEM\202308_1d.pickle
    WIPRO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_WIPRO\202308_1d.pickle
    HAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HAL\202308_1d.pickle
    ONGC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ONGC\202308_1d.pickle
    BAJFINANCE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BAJFINANCE\202308_1d.pickle
    TORNTPHARM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPHARM\202308_1d.pickle
    CONCOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CONCOR\202308_1d.pickle
    IDFCFIRSTB
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IDFCFIRSTB\202308_1d.pickle
    COALINDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COALINDIA\202308_1d.pickle
    BPCL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BPCL\202308_1d.pickle
    UPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_UPL\202308_1d.pickle
    TRENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TRENT\202308_1d.pickle
    INDIAMART
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIAMART\202308_1d.pickle
    MARUTI
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MARUTI\202308_1d.pickle
    AMBUJACEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMBUJACEM\202308_1d.pickle
    SHREECEM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SHREECEM\202308_1d.pickle
    DELTACORP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DELTACORP\202308_1d.pickle
    DRREDDY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_DRREDDY\202308_1d.pickle
    TVSMOTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TVSMOTOR\202308_1d.pickle
    ZEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ZEEL\202308_1d.pickle
    APOLLOHOSP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOHOSP\202308_1d.pickle
    AUBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUBANK\202308_1d.pickle
    INDHOTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDHOTEL\202308_1d.pickle
    RBLBANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_RBLBANK\202308_1d.pickle
    MRF
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MRF\202308_1d.pickle
    HEROMOTOCO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HEROMOTOCO\202308_1d.pickle
    MUTHOOTFIN
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MUTHOOTFIN\202308_1d.pickle
    FSL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FSL\202308_1d.pickle
    INDUSINDBK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDUSINDBK\202308_1d.pickle
    OFSS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OFSS\202308_1d.pickle
    PVR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PVR\202308_1d.pickle
    TATASTEEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATASTEEL\202308_1d.pickle
    AMARAJABAT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AMARAJABAT\202308_1d.pickle
    GODREJPROP
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GODREJPROP\202308_1d.pickle
    GAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GAIL\202308_1d.pickle
    FEDERALBNK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FEDERALBNK\202308_1d.pickle
    BIOCON
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BIOCON\202308_1d.pickle
    SAIL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SAIL\202308_1d.pickle
    SUNTV
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SUNTV\202308_1d.pickle
    EICHERMOT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_EICHERMOT\202308_1d.pickle
    CANFINHOME
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_CANFINHOME\202308_1d.pickle
    LT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_LT\202308_1d.pickle
    BEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BEL\202308_1d.pickle
    HCLTECH
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_HCLTECH\202308_1d.pickle
    BHEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHEL\202308_1d.pickle
    SBICARD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_SBICARD\202308_1d.pickle
    MANAPPURAM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MANAPPURAM\202308_1d.pickle
    JUBLFOOD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JUBLFOOD\202308_1d.pickle
    BHARATFORG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BHARATFORG\202308_1d.pickle
    METROPOLIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_METROPOLIS\202308_1d.pickle
    TORNTPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TORNTPOWER\202308_1d.pickle
    MCX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MCX\202308_1d.pickle
    GUJGASLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GUJGASLTD\202308_1d.pickle
    APOLLOTYRE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APOLLOTYRE\202308_1d.pickle
    INDIGO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_INDIGO\202308_1d.pickle
    TECHM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TECHM\202308_1d.pickle
    JINDALSTEL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_JINDALSTEL\202308_1d.pickle
    NATIONALUM
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NATIONALUM\202308_1d.pickle
    MPHASIS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MPHASIS\202308_1d.pickle
    M&M
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_M&M\202308_1d.pickle
    PERSISTENT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_PERSISTENT\202308_1d.pickle
    APLLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_APLLTD\202308_1d.pickle
    OBEROIRLTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_OBEROIRLTY\202308_1d.pickle
    MGL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_MGL\202308_1d.pickle
    IEX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_IEX\202308_1d.pickle
    ATUL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ATUL\202308_1d.pickle
    TATAMOTORS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAMOTORS\202308_1d.pickle
    GLENMARK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GLENMARK\202308_1d.pickle
    AUROPHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_AUROPHARMA\202308_1d.pickle
    GSPL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GSPL\202308_1d.pickle
    NAM-INDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NAM-INDIA\202308_1d.pickle
    COFORGE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_COFORGE\202308_1d.pickle
    ASHOKLEY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_ASHOKLEY\202308_1d.pickle
    TATAPOWER
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_TATAPOWER\202308_1d.pickle
    BOSCHLTD
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BOSCHLTD\202308_1d.pickle
    VEDL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_VEDL\202308_1d.pickle
    

---
---

# Downloading data for Various Index


```python
symbols = ['NIFTY', 'BANKNIFTY', 'GOLDBEES', 'INDIA VIX']
exchs = ['N','N', 'N', 'N']
exchs_type = ['C','C', 'C', 'D']
sl1 = []
for sym,e,et in zip(symbols,exchs,exchs_type):    
    s1 = fm.Stock(symbol=sym,exchange=e,exchange_type=et,store_local=True,local_data_foldpath=market_data_foldpath)
    sl1.append(s1)

nifty_sectors = ['NIFTY IT','NIFTY REALTY','NIFTY INFRA','NIFTY ENERGY','NIFTY FMCG','NIFTY MNC','NIFTY PHARMA','NIFTY PSE','NIFTY PSU BANK','NIFTY SERV SECTOR','NIFTY PVT BANK','NIFTY AUTO','FINNIFTY','NIFTY METAL','NIFTY HEALTHCARE','NIFTY OIL AND GAS','NIFTY TOTAL MARKET','NIFTY INDIA DIGITAL','NIFTYMEDIA']
nifty_gsecs = ['NIFTY GS 10YR','NIFTY GS 4 8YR','NIFTY GS 11 15YR','NIFTY GS 15YRPLUS','NIFTY GS COMPSITE']
for sym in nifty_sectors+nifty_gsecs:
    s1 = fm.Stock(symbol=sym,exchange="N",exchange_type="C",store_local=True,local_data_foldpath=market_data_foldpath)
    sl1.append(s1)

sm1 = scrip_master.get_scrip(sl1)

### start and end dates
# start = dtm.datetime(2019, 4, 1)
# end = dtm.datetime(2023, 4, 19)
```


```python
### 1 min data
dt1 = start
while dt1 <= end:
    start_date = dt1
    end_date = dt1 + dtm.timedelta(days=30)
    for s1 in sl1:
        n_try = 0
        while n_try < 20:
            try:
                c_5p.download_historical_data(stocklist=[s1], interval="1m", start=start_date, end=end_date)
                break
            except KeyboardInterrupt:
                raise KeyboardInterrupt
            except:
                n_try += 1
                print(n_try)
    dt1 = end_date

### 5 min data
dt1 = start
while dt1 <= end:
    start_date = dt1
    end_date = dt1 + dtm.timedelta(days=90)
    for s1 in sl1:
        n_try = 0
        while n_try < 20:
            try:
                c_5p.download_historical_data(stocklist=[s1], interval="5m", start=start_date, end=end_date)
                break
            except KeyboardInterrupt:
                raise KeyboardInterrupt
            except:
                n_try += 1
                print(n_try)
    dt1 = end_date


### daily data
for s1 in sl1:
    n_try = 0
    while n_try < 20:
        try:
            c_5p.download_historical_data(stocklist=[s1], interval="1d", start=start, end=end)
            break
        except KeyboardInterrupt:
            raise KeyboardInterrupt
        except:
            n_try += 1
            print(n_try)
```

    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202305_1m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202305_1m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202305_1m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202305_1m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202305_1m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202305_1m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202305_1m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202305_1m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202305_1m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202305_1m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202305_1m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202305_1m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202305_1m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202305_1m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202305_1m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202305_1m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202305_1m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202305_1m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202305_1m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202305_1m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202305_1m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202305_1m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202305_1m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202305_1m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202305_1m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202305_1m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202305_1m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202305_1m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202306_1m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202306_1m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202306_1m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202306_1m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202306_1m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202306_1m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202306_1m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202306_1m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202306_1m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202306_1m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202306_1m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202306_1m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202306_1m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202306_1m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202306_1m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202306_1m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202306_1m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202306_1m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202306_1m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202306_1m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202306_1m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202306_1m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202306_1m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202306_1m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202306_1m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202306_1m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202306_1m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202306_1m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202307_1m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202307_1m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202307_1m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202307_1m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202307_1m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202307_1m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202307_1m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202307_1m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202307_1m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202307_1m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202307_1m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202307_1m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202307_1m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202307_1m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202307_1m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202307_1m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202307_1m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202307_1m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202307_1m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202307_1m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202307_1m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202307_1m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202307_1m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202307_1m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202307_1m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202307_1m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202307_1m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202307_1m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202308_1m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202308_1m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202308_1m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202308_1m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202308_1m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202308_1m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202308_1m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202308_1m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202308_1m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202308_1m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202308_1m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202308_1m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202308_1m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202308_1m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202308_1m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202308_1m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202308_1m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202308_1m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202308_1m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202308_1m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202308_1m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202308_1m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202308_1m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202308_1m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202308_1m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202308_1m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202308_1m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202308_1m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202307_5m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202307_5m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202307_5m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202307_5m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202307_5m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202307_5m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202307_5m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202307_5m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202307_5m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202307_5m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202307_5m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202307_5m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202307_5m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202307_5m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202307_5m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202307_5m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202307_5m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202307_5m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202307_5m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202307_5m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202307_5m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202307_5m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202307_5m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202307_5m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202307_5m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202307_5m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202307_5m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202305_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202306_5m.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202307_5m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202308_5m.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202308_5m.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202308_5m.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202308_5m.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202308_5m.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202308_5m.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202308_5m.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202308_5m.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202308_5m.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202308_5m.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202308_5m.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202308_5m.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202308_5m.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202308_5m.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202308_5m.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202308_5m.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202308_5m.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202308_5m.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202308_5m.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202308_5m.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202308_5m.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202308_5m.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202308_5m.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202308_5m.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202308_5m.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202308_5m.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202308_5m.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202308_5m.pickle
    NIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY\202308_1d.pickle
    BANKNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_BANKNIFTY\202308_1d.pickle
    GOLDBEES
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_GOLDBEES\202308_1d.pickle
    INDIA VIX
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_D_INDIA VIX\202308_1d.pickle
    NIFTY IT
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY IT\202308_1d.pickle
    NIFTY REALTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY REALTY\202308_1d.pickle
    NIFTY INFRA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INFRA\202308_1d.pickle
    NIFTY ENERGY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY ENERGY\202308_1d.pickle
    NIFTY FMCG
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY FMCG\202308_1d.pickle
    NIFTY MNC
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY MNC\202308_1d.pickle
    NIFTY PHARMA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PHARMA\202308_1d.pickle
    NIFTY PSE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSE\202308_1d.pickle
    NIFTY PSU BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PSU BANK\202308_1d.pickle
    NIFTY SERV SECTOR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY SERV SECTOR\202308_1d.pickle
    NIFTY PVT BANK
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY PVT BANK\202308_1d.pickle
    NIFTY AUTO
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY AUTO\202308_1d.pickle
    FINNIFTY
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_FINNIFTY\202308_1d.pickle
    NIFTY METAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY METAL\202308_1d.pickle
    NIFTY HEALTHCARE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY HEALTHCARE\202308_1d.pickle
    NIFTY OIL AND GAS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY OIL AND GAS\202308_1d.pickle
    NIFTY TOTAL MARKET
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY TOTAL MARKET\202308_1d.pickle
    NIFTY INDIA DIGITAL
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY INDIA DIGITAL\202308_1d.pickle
    NIFTYMEDIA
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTYMEDIA\202308_1d.pickle
    NIFTY GS 10YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 10YR\202308_1d.pickle
    NIFTY GS 4 8YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 4 8YR\202308_1d.pickle
    NIFTY GS 11 15YR
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 11 15YR\202308_1d.pickle
    NIFTY GS 15YRPLUS
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS 15YRPLUS\202308_1d.pickle
    NIFTY GS COMPSITE
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202305_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202306_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202307_1d.pickle
    Creating the file - C:\Users\GTCRL\Indian Institute of Science\We Will - Documents\General\market\Finmetry\data\local_data\N_C_NIFTY GS COMPSITE\202308_1d.pickle
    

---
---
