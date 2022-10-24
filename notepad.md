**remove duplicate lines**
find ^(.*?)$\s+?^(?=.*^\1$)
replace ""
