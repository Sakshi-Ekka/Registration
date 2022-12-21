# Registration
School Admission form built using python and MySql (School Project)



import mysql.connector as mys

mycon = mys.connect(host='localhost',user = 'root',passwd='student123',database='School')
mycur = mycon.cursor()


def display():
    query = 'select * from School_Admission'
    mycur.execute(query)
    data = mycur.fetchall()
    print("______________________________________________________________________________________________________________________________________________________________________")
    print("")
    print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> Student's Details <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<")
    print("")
    print("")
    print ("                *******************************************************************************************************************")
    print ("                * ","Admission No."," * "," Name","               *","Class","     *","DOB","             *","Address","            *","DOA","            *")
    print ("                *******************************************************************************************************************")
    for a,b,c,d,e,f in data:
        print ("                *  ",a,"        *"," ",b,"        *",c,"        *",d,"     *",e,"        *",f)
    print ("                *******************************************************************************************************************")
    print("")
    print("_______________________________________________________________________________________________________________________________________________________________________")



def addnew():
    print('')
    print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>> Add New Student <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<")
    print('')
    print("++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++ Enter details of new student +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++")
    print('')
    import random
    r=random.randint(40000,0000)
    adn=r
    print("       Admission Number: ",adn)
    print("")
    nm=input("       Enter Name: ")
    print("")
    cls=int(input("       Enter Class: "))
    print("")
    dob=input("       Enter DOB(YYYY-MM-DD): ")
    print("")
    adr=input("       Enter Address: ")
    print("")
    doa=input("       Enter DOA(YYYY-MM-DD): ")
    print("")
    print("       Student's details successfully added.")
    print("+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++")
    print("")
    query="insert into School_Admission values({},'{}',{},'{}','{}','{}')".format(adn,nm,cls,dob,adr,doa)
    mycur.execute(query)
    mycon.commit()
    



def modify():
    print('')
    print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>  Modify Student's Details  <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<")
    print('')
    adn=int(input("       Enter Admission Number to Modify: "))
    query="select * from School_Admission"
    mycur.execute(query)
    data = mycur.fetchall()
    k = []
    for i in data:
        k.append(i[0])
    if adn in k:
        print ("")
        print("       1. Modify Name")
        print("       2. Modify DOB")
        print("       3. Modify Address")
        print("")
        ch = int(input("       ENTER YOUR CHOICE: "))
        print("")
        mycur.execute("select * from School_Admission where Adm_No={}".format(adn))
        D = mycur.fetchall()
        for a,b,c,d,e,f in D:
            print("")
        if ch == 1:
            print("       Current Name: ",b)
            print("")
            nm=input("       Change Name To: ")
            query="update School_Admission set Name='{}' where Adm_No={}".format(nm,adn)
        elif ch == 2:
            print("       Current DOB: ",d)
            dob=input("       Change DOB To: ")
            query="update School_Admission set DOB='{}' where Adm_No={}".format(dob,adn)
        elif ch == 3:
            print("       Current Address: ",e)
            adr=input("       Change Address To: ")
            query="update School_Admission set Address='{}' where Adm_No={}".format(adr,adn)
        else:
            print("       Invalid Choice")
        print("")    
        print("       Student's details successfully modified.")    
        mycur.execute(query)
        mycon.commit()
            
        
    else:
        print("")
        print("       -X-X-X__Admission Number number does not exists__X-X-X-")
     
    

def delete():
    print("")
    print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>  Delete Student's Details  <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<")
    print("")
    adn=int(input("       Enter Admission Number to Delete: "))
    query= 'select * from School_Admission where Adm_No ={}'.format(adn)
    mycur.execute(query)
    data = mycur.fetchall()
    if mycur.rowcount <=0:
        print("")
        print("       -X-X-X__Admission Number number does not exists__X-X-X-")
    

    for a,b,c,d,e,f in data:
        
        print("")
        print("                  Admission Number      Name                  Class      DOB              Address             DOA")
        print("")
        print ("       Details:"," ",a,"               ",b,"          ",c,"      ",d,"      ",e,"          ",f)
        print("")
        ch=input("       Are you sure to delete(y/n): ")
        if ch=='y':
            query='delete from School_Admission where Adm_No={}'.format(adn)
            mycur.execute(query)
            mycon.commit()
            print("")
            print("       Successfully Deleted")
        elif ch =='n':
            print("")
            print("       Deletion Cancelled !!!")

           
   



def search():
    print("")
    print(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>  Search Student's Details  <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<")
    print("")
    adn=int(input("       Enter Admission Number to Search: "))
    query = 'select * from School_Admission where Adm_No={}'.format(adn)
    mycur.execute(query)
    data = mycur.fetchall()
    for a,b,c,d,e,f in data:
        print("")
    if mycur.rowcount <=0:
        print("")
        print("       -X-X-X__Admission Number number does not exists__X-X-X-")
        print("")
    else:
        print("")
        print("         Admission Number        Name               Class          DOB               Address               DOA")
        print("")
        print ("        ",a,"                 ", b,"      ",c,"           ",d,"      ",e,"              ",f)
        print("")
        
    
    
    
    
    


print("")
print("")
print('~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ STUDENT ADMISSION ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~')
print("                                                                          DAV RAIGARH                                                                              ")


if mycon.is_connected():
    print("")

while True:
    print("")
    print("^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^")
    print("")
    print("      School Management Menu")
    print("")
    print("       1. Display")
    print("")
    print("       2. Add New")
    print("")
    print("       3. Modify")
    print("")
    print("       4. Delete")
    print("")
    print("       5. Search")
    print("")
    print("       6. Exit")
    print("")
    print("-----------------------------------------------------------------------------------------------------------------------------------------------------------------------")
    print('')

    ch = int(input("       ENTER YOUR CHOICE: "))
    if ch == 1:
        display()
       
    elif ch == 2:
        addnew()
        
    elif ch == 3:
        modify()
       
    elif ch == 4:
        delete()
        
    elif ch == 5:
        search()
       
    elif ch == 6:
        print("")
        print("-----------------------------------------------------------------------------------------------------------------------------------------------------------------------")
        print("")
        print("       Thank you for visiting.",end=""),print("","\U0001F60A")
        print("")
        print("'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''")
        break
    else :
        print("")
        print("       Invalid Choice !!!")
        print("")
        
      

    

