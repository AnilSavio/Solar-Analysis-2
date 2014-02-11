Solar-Analysis-2
================
import numpy as np
import os
import fnmatch
import fileinput
import pandas as pd
from pandas import *
from pandas import DataFrame
import glob
import fnmatch
import matplotlib.pyplot as plt
import datetime as dt
from datetime import datetime
from dateutil.parser import parse

class getyear:
    def get_year(self, years):
        self.years=years

        rootdir='E:\\time_series_hourly_dni\\'

        fileyear= pd.DataFrame()

        for dirName, subdirList, fileList in os.walk(rootdir):

            for fname in fileList:
                splitName=fname.split('_')
                month = int(splitName[2][4:6])
                day=int(splitName[2][6:8])

                year1=int(splitName[2][0:4])

                hour=int(splitName[3][0:2])
                yearmonthday=parse(splitName[2][0:8])


                time=dt.time(hour)
                timestamp=dt.datetime.combine(yearmonthday, time)

                for year in years:
                    if year1==year:

                        filePath=os.path.join(dirName,fname)
                        
                        DNI=fileyear.append(pd.read_csv(filePath, sep='\s', skiprows=6))
                        DNI.replace(-999,0, inplace=True)



                        print DNI.ix[500,600], timestamp

                        for i in DNI:
                        DNI_0=(pd.concat(DNI))
                        print DNI_0

                        
                        x=timestamp
                        y=DNI_0.ix[500,600]
                        print x,y
                        fig=plt.figure()
                        ax=fig.add_subplot(1,1,1)
                        ax.scatter(x,y)
                        plt.show()
                                              
                              
z=getyear()
print z.get_year(range(2000,2004))
