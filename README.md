# Flames
# Flames is a love calculator that defines acronyms that gives your relationship status with your crush
from tkinter import *

def delete_same_characters(name1,name2):  
    for i in range(len(name1)) :  
        for j in range(len(name2)) :  

            if name1[i] == name2[j] :  
                substitute = name1[i]  
                name1.remove(substitute)  
                name2.remove(substitute)  
                list = name1 + ["*"] + name2   
                return [list,True]  
  
    list = name1 + ["*"] + name2  
    return [list,False]  

def get_status() :  
    your = your_field.get()  
    your = your.lower()  
    your.replace(" " , "")  
    your_list = list(your)  
    crush = crush_field.get()  
    crush = crush.lower()  
    crush.replace(" " , "")  
    crush_list = list(crush)  

    initialised = True  
    while initialised :  
        final_list = delete_same_characters(your_list , crush_list)  
        concatenated_list = final_list[0]  
        # taking out the flag value from the return list  
        initialised = final_list[1]  
        # finding the index of "*" / border mark  
        str_index = concatenated_list.index("*")  
        # performing list slicing  
        # all chars before * stored in your_list  
        your_list = concatenated_list[ : str_index]  
        # all chars after * store in crush_list  
        crush_list = concatenated_list[str_index + 1 : ]  
  
    count = len(your_list) + len(crush_list)  
    result = ["Friends" , "Love" , "Affection" , "Marriage" , "Enemy" , "Siblings"]  
  
    while len(result) > 1 :  
        cover_index = (count % len(result) - 1)  
        if cover_index >= 0 :  
            right = result[cover_index + 1 : ]  
            left = result[ : cover_index]  
            result = right + left  
        else :  
            result = result[ : len(result) - 1]  
          
        # using the insert method to insert the  
        # value in the text entry box   
    status_field.insert(10, result[0])  
    
def clear_all():  
    your_field.delete(0 , END)  
    crush_field.delete(0 , END)  
    status_field.delete(0 , END)  
 
    your_field.focus_set() 
    #focus_set is used here to get focus on your_field because all data are cleared so now we have to put values or names again
    

if _name_ == "_main_" :  
    master = Tk()  
    master.configure(background = 'black')  
    master.geometry("400x170")  
    master.title("Flames")  
    l1 = Label(master,text = "  Your Name: ",fg ='black',bg = 'white')  #11
    l2 = Label(master , text = "Crush Name: ",fg = 'black',bg = 'white')#11  
    l3 = Label(master , text = "Relationship Status: " ,fg = 'black' , bg = 'white')  
    l1.grid(row = 1 , column = 0 , sticky = "E")  
    l2.grid(row = 2 , column = 0 , sticky = "E")  
    l3.grid(row = 4 , column = 0 , sticky = "E")  
  
    your_field = Entry(master)  
    crush_field = Entry(master)  
    status_field = Entry(master)  

    your_field.grid(row = 1 , column = 1 , ipadx = "50")  
    crush_field.grid(row = 2 , column = 1 , ipadx = "50")  
    status_field.grid(row = 4 , column = 1 , ipadx = "50")  
    #ipadx?
    button1 = Button(master , text = "Submit" , bg = "red",fg = "black" , command = get_status)    
    button2 = Button(master , text = "Clear" , bg = "red",fg = "black" , command = clear_all)  
  
    button1.grid(row = 3 , column = 1)  
    button2.grid(row = 5 , column = 1)  
    master.mainloop()
