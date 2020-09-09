# code-vaizle
days_in_months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 ] 
  
def numberOfLeapYears(year ,month ,date):     
    years = year
    if(month <= 2): 
        years -= 1
            
    return int(years / 4 - years / 100 + years / 400 ) 
  
 
def numberOfDays(dt1, dt2) : 
    dt1y = dt1[0]
    dt1m = dt1[1]
    dt1d = dt1[2]
 
    dt2y = dt2[0]
    dt2m = dt2[1]
    dt2d = dt2[2]
 
 
    n1 = dt1y * 365 + dt1d  
    for i in range(0, dt1m - 1) : 
        n1 += days_in_months[i]  
    n1 += numberOfLeapYears(dt1y,dt1m,dt1d)
  
 
    n2 = dt2y * 365 + dt2d  
    for i in range(0, dt2m - 1) : 
        n2 += days_in_months[i]  
    n2 += numberOfLeapYears(dt2y,dt2m,dt2d)
    if(( ( (dt2y % 4 == 0) and (dt2y % 100 != 0)) or (dt2y % 400 == 0) ) and dt2m >= 3 ):
        n2+=1
 
    return (n2 - n1)  
 
 
 
 
 
 
 
def dateToDay(year,month,date):
    
    #Jan 1st 1970 was a Thursday
    
    days_of_week = ["Thu" ,"Fri" ,"Sat" ,"Sun" ,"Mon" ,"Tue" ,"Wed"]
    base = numberOfDays([1970 , 1, 1] , [year ,month ,date] )
    return days_of_week[ base%7 ]
 
    
 
 
#print(dateToDay(2020,2,29))
#print(dateToDay(2020,3,1))
 
 
def solution(D):
    output = { "Mon" : -1,"Tue" :-1,"Wed" : -1,"Thu" : -1,"Fri" : -1,"Sat" : -1,"Sun" : -1 }
    
    for i in D.keys():
        date = i.split('-')
        day = dateToDay(int(date[0]),int(date[1]),int(date[2]) )
 
        if(output[day] == -1):
            output[day] += 1
        
        output[day] += D[i]
    keys = list(output.keys())
    for i in range(len(keys) ):
        if(output[keys[i]] == -1 ):
            output[keys[i]] = ( output[keys[ (i - 1)%7 ] ] + output[keys[ (i + 1)%7 ] ] ) // 2
    return output
 
 
#print(solution({'2020-01-01':4,'2020-01-02':5,'2020-01-03':6,'2020-01-04':8,'2020-01-05':2,'2020-01-06':7}))
