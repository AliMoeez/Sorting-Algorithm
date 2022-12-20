from tkinter import *
import matplotlib.pyplot as plt
from matplotlib.backends.backend_tkagg import (FigureCanvasTkAgg, NavigationToolbar2Tk)
import datetime

SCREEN=Tk()

SCREEN.geometry("1100x900")

SCREEN.config(bg="SteelBlue1")

SCREEN_CANVAS=Canvas(SCREEN,height=450,width=800,bg="WHITE")
SCREEN_CANVAS.pack(pady=90)

title=Label(SCREEN,text="Sorting Algorithm",bg="SteelBlue1")
title.config(font=("arial",25))
title.place(x=430,y=20)

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
list_axis=["Number 1","Number 2","Number 3","Number 4","Number 5"]

validation_condition_S_1=False
validation_condition_S_2=False
validation_condition_S_3=False

validation_condition_2=False

sorting_condition_1=False
sorting_condition_2=False
sorting_condition_3=False

another_sort=False

user_entry=''

class Buttons:
    def user_input_run(self,entry_one_string,entry_two_string,entry_three_string,entry_four_string,entry_five_string,user_entry):
       # global user_entry
        self.entry_one_string=entry_one_string ; self.entry_two_string=entry_two_string ; self.entry_three_string=entry_three_string 
        self.entry_four_string=entry_four_string ; self.entry_five_string=entry_five_string ; self.user_entry=user_entry

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
    def validation_of_input(self,validation_on_S_1,validation_condition_S_2,validation_condition_S_3,validation_condition_2,
                            sorting_condition_1,sorting_condition_2,sorting_condition_3,list_entry,list_axis,another_sort):
        self.validation_condition_S_1=validation_condition_S_1 ; self.validation_condition_S_2=validation_condition_S_2 ; self.validation_condition_S_3=validation_condition_S_3
        self.validation_condition_2=validation_condition_2
        self.sorting_condition_1=sorting_condition_1; self.sorting_condition_2=sorting_condition_2 ; self.sorting_condition_3=sorting_condition_3
        self.entry_sort_string=entry_sort_string ; self.user_entry=user_entry
        self.entry_one_string=entry_one_string ; self.entry_two_string=entry_two_string ; self.entry_three_string=entry_three_string 
        self.entry_four_string=entry_four_string ; self.entry_five_string=entry_five_string ; self.list_entry=list_entry ; self.list_axis=list_axis ; self.another_sort=another_sort
        
    def check_validation(self):
        global list_entry_copy, list_entry_copy_sort , list_axis_copy, time_difference_in_sort_1, time_difference_in_sort_2, time_difference_in_sort_3
        global canvas_label_before, canvas_label_after
        if self.entry_sort_string.get()=="Quick Sort":
            self.validation_condition_S_1=True   
            self.validation_condition_S_2=False ; self.validation_condition_S_3=False
        if self.entry_sort_string.get()=="Bubble Sort":
            self.validation_condition_S_2=True 
            self.validation_condition_S_1=False ; self.validation_condition_S_3=False
        if self.entry_sort_string.get()=="Selection Sort":
            self.validation_condition_S_3=True
            self.validation_condition_S_1=False ; self.validation_condition_S_2=False
            
        if (not self.entry_one_string.get()=="--" and not self.entry_two_string.get()=="--" and not self.entry_three_string.get()=="--" and 
            not self.entry_four_string.get()=="--" and not self.entry_five_string.get()=="--"):
            self.validation_condition_2=True
            
        if self.validation_condition_S_1 and self.validation_condition_2:
            self.sorting_condition_1=True
            self.sorting_condition_2=False ; self.sorting_condition_3=False
            self.list_entry.append(int(self.entry_one_string.get())) ; self.list_entry.append(int(self.entry_two_string.get()))
            self.list_entry.append(int(self.entry_three_string.get())) ; self.list_entry.append(int(self.entry_four_string.get())) ; self.list_entry.append(int(self.entry_five_string.get()))
            print(self.list_entry)
            if button_validation_results["state"]==NORMAL:
                button_validation_results["state"]=DISABLED
            else:
                button_validation_results["state"]=NORMAL 
            
            #figure for plot before quick sorting
            timer_before_sort_1=datetime.datetime.now()
            figure=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(self.list_axis,self.list_entry)
            canvas_for_graph=FigureCanvasTkAgg(figure,master=SCREEN)
            canvas_for_graph.get_tk_widget().place(x=150,y=180)
            canvas_label_before=Label(SCREEN,text="List Before Quick Sort",bg="White")
            canvas_label_before.place(x=200,y=150)
            canvas_label_before.config(font=("arial",20))
            
            #code to turn unsorted list to a sorted one using quick sort
            lists_small=[] ; lists_mid=[] ; lists_big=[]
            lists_small_string=[] ; lists_mid_string=[] ; lists_big_string=[]
            pivot_number=self.list_entry[2]
            for i in range(len(self.list_entry)):
                if self.list_entry[i]>pivot_number:
                    lists_big.append(self.list_entry[i]) ; lists_big_string.append(self.list_axis[i])
                if self.list_entry[i]<pivot_number:
                    lists_small.append(self.list_entry[i]) ; lists_small_string.append(self.list_axis[i])
                if self.list_entry[i]==pivot_number:
                    lists_mid.append(self.list_entry[i]) ; lists_mid_string.append(self.list_axis[i])
            for i in range(len(lists_small)):   
                for q in range(len(lists_small)-i-1):
                    if lists_small[q]>lists_small[q+1]:
                        lists_small[q],lists_small[q+1]=lists_small[q+1],lists_small[q] ; lists_small_string[q],lists_small_string[q+1]=lists_small_string[q+1],lists_small_string[q]
            for i in range(len(lists_big)):
                for q in range(len(lists_big)-i-1):
                    if lists_big[q]>lists_big[q+1]:
                        lists_big[q],lists_big[q+1]=lists_big[q+1],lists_big[q] ; lists_big_string[q],lists_big_string[q+1]=lists_big_string[q+1],lists_big_string[q]
            lists_new=lists_small+lists_mid+lists_big ; lists_new_string=lists_small_string+lists_mid_string+lists_big_string
            timer_after_sort_1=datetime.datetime.now()
            time_difference_in_sort_1=timer_after_sort_1-timer_before_sort_1
    
            #figure for plot after adding quick sort 
            figure_new=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(lists_new_string,lists_new)
            canvas_for_completed_graph=FigureCanvasTkAgg(figure_new,master=SCREEN)
            canvas_for_completed_graph.get_tk_widget().place(x=550,y=180)
            canvas_label_after=Label(SCREEN,text="List After Quick Sort",bg="White")
            canvas_label_after.place(x=600,y=150)
            canvas_label_after.config(font=("arial",20))
            self.another_sort=True
            print(self.another_sort)
            #code for user to choose another set of numbers to sort
     
        if self.validation_condition_S_2 and self.validation_condition_2:
            self.sorting_condition_2=True 
            self.sorting_condition_1=False ; self.sorting_condition_3=False
            self.list_entry.append(int(self.entry_one_string.get())) ; self.list_entry.append(int(self.entry_two_string.get()))
            self.list_entry.append(int(self.entry_three_string.get())) ; self.list_entry.append(int(self.entry_four_string.get())) ; self.list_entry.append(int(self.entry_five_string.get()))
            if button_validation_results["state"]==NORMAL:
                button_validation_results["state"]=DISABLED
            else:
                button_validation_results["state"]=NORMAL 
                
            #figure for plot before bubble sorting
            timer_before_sort_2=datetime.datetime.now()
            figure=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(self.list_axis,self.list_entry)
            canvas_for_graph=FigureCanvasTkAgg(figure,master=SCREEN)
            canvas_for_graph.get_tk_widget().place(x=150,y=180)
            canvas_label_before=Label(SCREEN,text="List Before Bubble Sort",bg="White")
            canvas_label_before.place(x=200,y=150)
            canvas_label_before.config(font=("arial",20))
            
            #code for bubble sort
            for i in range(len(self.list_entry)):
                for q in range(len(self.list_entry)-i-1):
                    if self.list_entry[q]>self.list_entry[q+1]:
                        self.list_entry[q],self.list_entry[q+1]=self.list_entry[q+1],self.list_entry[q]
                        self.list_axis[q],self.list_axis[q+1]=self.list_axis[q+1],self.list_axis[q]
            timer_after_sort_2=datetime.datetime.now()
            time_difference_in_sort_2=timer_after_sort_2-timer_before_sort_2
            #code for new plot
            figure_new=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(self.list_axis,self.list_entry)
            canvas_for_completed_graph=FigureCanvasTkAgg(figure_new,master=SCREEN)
            canvas_for_completed_graph.get_tk_widget().place(x=550,y=180)
            canvas_label_after=Label(SCREEN,text="List After Bubble Sort",bg="White")
            canvas_label_after.place(x=600,y=150)
            canvas_label_after.config(font=("arial",20))
            self.another_sort=True
            print(self.another_sort)                
            
        if self.validation_condition_S_3 and self.validation_condition_2:
            self.sorting_condition_3=True
            self.sorting_condition_1=False ; self.sorting_condition_2=False
            self.list_entry.append(int(self.entry_one_string.get())) ; self.list_entry.append(int(self.entry_two_string.get()))
            self.list_entry.append(int(self.entry_three_string.get())) ; self.list_entry.append(int(self.entry_four_string.get())) ; self.list_entry.append(int(self.entry_five_string.get()))
            
            #figure for plot before selection sort sorting
            figure=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(self.list_axis,self.list_entry)
            canvas_for_graph=FigureCanvasTkAgg(figure,master=SCREEN)
            canvas_for_graph.get_tk_widget().place(x=150,y=180)
            canvas_label_before=Label(SCREEN,text="List Before Selection Sort",bg="White")
            canvas_label_before.place(x=200,y=150)
            canvas_label_before.config(font=("arial",20))
            
            #code for selection sort
            timer_before_sort_3=datetime.datetime.now()
            list_entry_copy=self.list_entry[:]
            list_axis_copy=[]
            list_entry_copy_sort=[]
            
            for i in range(len(list_entry_copy)):
                list_entry_copy_sort.append(min(list_entry_copy))
                list_axis_copy.append(self.list_axis[i])
                list_entry_copy.remove(min(list_entry_copy))
            timer_after_sort_3=datetime.datetime.now()
            time_difference_in_sort_3=timer_after_sort_3-timer_before_sort_3
                
            #code for selection sort
            figure_new=plt.figure(figsize=(5,5))
            plt.subplot(111)
            plt.bar(list_axis_copy,list_entry_copy_sort)
            canvas_for_completed_graph=FigureCanvasTkAgg(figure_new,master=SCREEN)
            canvas_for_completed_graph.get_tk_widget().place(x=550,y=180)
            canvas_label_after=Label(SCREEN,text="List After Selection Sort",bg="White")
            canvas_label_after.place(x=600,y=150)
            canvas_label_after.config(font=("arial",20))
            self.another_sort=True
            print(self.another_sort)   
            
    def sorting_timer(self):
        global time_label_1, time_label_2, time_label_3
        try:
            if self.sorting_condition_1 is True:
                print("yes1")
                time_label_1=Label(SCREEN,text="The Time To Quick Sort Was :" + str(time_difference_in_sort_1), bg="SteelBlue1")
                time_label_1.place(x=390,y=800)
            if self.sorting_condition_2 is True:
                print("yes2")
                time_label_2=Label(SCREEN,text="The Time To Bubble Sort Was :" + str(time_difference_in_sort_2), bg="SteelBlue1")
                time_label_2.place(x=390,y=800)
            if self.sorting_condition_3 is True:
                print("yes3")
                time_label_3=Label(SCREEN,text="The Time To Selection Sort Was :" + str(time_difference_in_sort_3), bg="SteelBlue1")
                time_label_3.place(x=390,y=800)
        except NameError: pass
        
    def sort_again(self):
        if self.another_sort is True:
            button_ask_again["state"]=NORMAL
        else:
            if button_ask_again["state"]==NORMAL:
                button_ask_again["state"]=DISABLED
                
    def sort_again_cond(self):
        if button_ask_again["state"]==NORMAL:
            self.list_entry.clear() ; self.list_axis.clear()
            list_entry_copy_sort.clear() ; list_entry_copy.clear() ; list_axis_copy.clear()
            canvas_label_before.destroy() ; canvas_label_after.destroy()
            try:
                time_label_1.destroy() 
            except: pass
            try:
                time_label_2.destroy()
            except: pass
            try:
                time_label_3.destroy()
            except: pass
            self.list_axis=["Number 1","Number 2","Number 3","Number 4","Number 5"]
            self.entry_one_string.set(entry_one[0]) ; self.entry_two_string.set(entry_two[0]) ; self.entry_three_string.set(entry_three[0])
            self.entry_four_string.set(entry_four[0]) ; self.entry_five_string.set(entry_five[0]) ; self.entry_sort_string.set(entry_sort[0])
            button_validation_results["state"]=NORMAL
          
display_numbers=Label(SCREEN,text="The Numbers You Want To Sort Are : " ,bg="Steelblue1")  
display_numbers.place(x=165,y=670)
display_choice_sort=Label(SCREEN,text="The Type of Sort You Want Is A -- ",bg="Steelblue1")
display_choice_sort.place(x=570,y=670)

buttons=Buttons()
buttons.user_input_run(entry_one_string,entry_two_string,entry_three_string,entry_four_string,entry_five_string,user_entry)
buttons.display_numbers()
buttons.sort_user_choice_input(entry_sort_string)

button_show_list=Button(SCREEN,text="Done!",command=buttons.display_numbers)
button_show_list.place(x=245,y=630) 
button_choose_sort_type=Button(SCREEN,text="Done!",command=buttons.sort_user_choice_show)
button_choose_sort_type.place(x=637,y=630)

sorting=Sorting()
sorting.validation_of_input(validation_condition_S_1,validation_condition_S_2,validation_condition_S_3,
                            validation_condition_2,sorting_condition_1,sorting_condition_2,sorting_condition_3,list_entry,list_axis,another_sort)
sorting.check_validation()
#sorting.sorting_timer()

#sorting.quick_sort()

button_validation_results=Button(SCREEN,text="Sort!",command=lambda:[sorting.check_validation(),sorting.sort_again(),sorting.sorting_timer()])
button_validation_results.place(x=470,y=720)

button_ask_again=Button(SCREEN,text="Do You Want To Sort Again?",command=lambda: [sorting.sort_again(),sorting.sort_again_cond()])
button_ask_again.place(x=415,y=755)

sorting.sort_again()

SCREEN.mainloop()
