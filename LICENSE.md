from pandas import *  
from ggplot import *

df = pandas.read_csv('./turnstile_data_master_with_weather.csv')

df['meandewpti'] = df['meandewpti'].map(lambda x: round((x-32.0)*(5.0/9.0),0))

daily = df.groupby(df.meandewpti).EXITSn_hourly.sum()  
daily.index.name = 'day'  
daily = daily.reset_index()

p = ggplot(daily, aes('day', weight='EXITSn_hourly',alpha=0.5)) + \  
geom_bar(fill="green") + \  
theme_xkcd() + \  
ggtitle("May 2011 - Turnstile Exits by Dew Point") + \  
xlab("Degrees Celsius") + \  
ylab("# of Exits")  
print p  
