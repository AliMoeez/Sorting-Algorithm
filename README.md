from tkinter import *

SCREEN=Tk()

SCREEN.geometry("1000x800")

SCREEN.config(bg="SteelBlue1")

SCREEN_CANVAS=Canvas(SCREEN,height=450,width=800,bg="WHITE")
SCREEN_CANVAS.pack(pady=90)

entry_one=["--",1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
entry_two=["--",1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
entry_three=["--",1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
entry_four=["--",1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]
entry_five=["--",1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]

entry_one_label=Label(SCREEN,text="Number 1", bg="SteelBlue1").place(x=95,y=550)
entry_one_string=StringVar(SCREEN) ; entry_one_string.set(entry_one[0])
entry_one_list=OptionMenu(SCREEN,entry_one_string,*entry_one).place(x=100,y=580)

entry_two_label=Label(SCREEN,text="Number 2", bg="SteelBlue1").place(x=165,y=550)
entry_two_string=StringVar(SCREEN) ; entry_two_string.set(entry_two[0])
entry_two_list=OptionMenu(SCREEN,entry_two_string,*entry_two).place(x=170,y=580)

entry_three_label=Label(SCREEN,text="Number 3", bg="SteelBlue1").place(x=235,y=550)
entry_three_string=StringVar(SCREEN) ; entry_three_string.set(entry_three[0])
entry_three_list=OptionMenu(SCREEN,entry_three_string,*entry_three).place(x=240,y=580)

entry_four_label=Label(SCREEN,text="Number 4", bg="SteelBlue1").place(x=305,y=550)
entry_four_string=StringVar(SCREEN) ; entry_four_string.set(entry_four[0])
entry_four_list=OptionMenu(SCREEN,entry_four_string,*entry_four).place(x=310,y=580)
                      
entry_five_label=Label(SCREEN,text="Number 5", bg="SteelBlue1").place(x=375,y=550)
entry_five_string=StringVar(SCREEN) ; entry_five_string.set(entry_five[0])
entry_five_list=OptionMenu(SCREEN,entry_five_string,*entry_five).place(x=380,y=580)

entry_sort=["--","Quick Sort","Bubble Sort", "Selection Sort"]

entry_sort_label=Label(SCREEN,text="Choose Your Sorting Type", bg="Steelblue1").place(x=600,y=550)
entry_sort_string=StringVar(SCREEN) ; entry_sort_string.set(entry_sort[0])
entry_sort_list=OptionMenu(SCREEN,entry_sort_string,*entry_sort).place(x=630,y=580)

list_entry=[]

validation_condition_S_1=False
validation_condition_S_2=False
validation_condition_S_3=False

validation_condition_2=False

sorting_condition_1=False
sorting_condition_2=False
sorting_condition_3=False

class Buttons:
    def user_input_run(self,entry_one_string,entry_two_string,entry_three_string,entry_four_string,entry_five_string):
        global user_entry
        self.entry_one_string=entry_one_string ; self.entry_two_string=entry_two_string ; self.entry_three_string=entry_three_string 
        self.entry_four_string=entry_four_string ; self.entry_five_string=entry_five_string

    def display_numbers(self):
        global button_show_list
        self.list_entry=list_entry
        self.user_entry=self.entry_one_string.get()+","+self.entry_two_string.get()+","+self.entry_three_string.get()+","+self.entry_four_string.get()+","+self.entry_five_string.get() 
        display_numbers.config(text="The Numbers You Want To Sort Are : "+self.user_entry)
    
    def sort_user_choice_input(self,entry_sort_string):
        self.entry_sort_string=entry_sort_string
        
    def sort_user_choice_show(self):
        display_choice_sort.config(text="The Type of Sort You Want Is A "+self.entry_sort_string.get())
        
class Sorting:
    def validation_of_input(self,validation_condition_S_1,validation_condition_S_2,validation_condition_S_3,validation_condition_2,sorting_condition_1,sorting_condition_2,sorting_condition_3):
        self.validation_condition_S_1=validation_condition_S_1 ; self.validation_condition_S_2=validation_condition_S_2 ; self.validation_condition_S_3=validation_condition_S_3
        self.validation_condition_2=validation_condition_2
        self.sorting_condition_1=sorting_condition_1; self.sorting_condition_2=sorting_condition_2 ; self.sorting_condition_3=sorting_condition_3
        self.entry_sort_string=entry_sort_string ; self.user_entry=user_entry
        self.entry_one_string=entry_one_string ; self.entry_two_string=entry_two_string ; self.entry_three_string=entry_three_string 
        self.entry_four_string=entry_four_string ; self.entry_five_string=entry_five_string
        
    def check_validation(self):
        
        if self.entry_sort_string.get()=="Quick Sort":
            self.validation_condition_S_1=True   
            self.validation_condition_S_2=False ; self.validation_condition_S_3=False
        if self.entry_sort_string.get()=="Bubble Sort":
            self.validation_condition_S_2=True 
            self.validation_condition_S_1=False ; self.validation_condition_S_3=False
        if self.entry_sort_string.get()=="Selection Sort":
            self.validation_condition_S_3=True
            self.validation_condition_S_1=False ; self.validation_condition_S_2=False
            
        if (not self.entry_one_string=="--" and not self.entry_two_string=="--" and not self.entry_three_string=="--" and 
            not self.entry_four_string=="--" and not self.entry_five_string=="--"):
            self.validation_condition_2=True
            
        if self.validation_condition_S_1 and self.validation_condition_2:
            self.sorting_condition_1=True
        if self.validation_condition_S_2 and self.validation_condition_2:
            self.sorting_condition_2=True 
        if self.validation_condition_S_3 and self.validation_condition_2:
            self.sorting_condition_3=True
  
        
        
display_numbers=Label(SCREEN,text="The Numbers You Want To Sort Are : " +user_entry,bg="Steelblue1")  
display_numbers.place(x=165,y=670)
display_choice_sort=Label(SCREEN,text="The Type of Sort You Want Is A -- ",bg="Steelblue1")
display_choice_sort.place(x=570,y=670)

buttons=Buttons()
buttons.user_input_run(entry_one_string,entry_two_string,entry_three_string,entry_four_string,entry_five_string)
buttons.display_numbers()
buttons.sort_user_choice_input(entry_sort_string)

button_show_list=Button(SCREEN,text="Done!",command=buttons.display_numbers)
button_show_list.place(x=245,y=630) 
button_choose_sort_type=Button(SCREEN,text="Done!",command=buttons.sort_user_choice_show)
button_choose_sort_type.place(x=637,y=630)

sorting=Sorting()
sorting.validation_of_input(validation_condition_S_1,validation_condition_S_2,validation_condition_S_3,validation_condition_2,sorting_condition_1,sorting_condition_2,sorting_condition_3)
sorting.check_validation()

button_validation_results=Button(SCREEN,text="Sort!",command=sorting.check_validation)
button_validation_results.place(x=470,y=720)

SCREEN.mainloop()
