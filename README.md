# Tkinter-Timer-Draft
#sqlite3 for database, tkinter as tk and webbroswer
GREAT BUTTON ICONS HERE: https://findicons.com/search/button/14

import sqlite3
import tkinter as tk 
import webbrowser

class Timer:
    def __init__(self, root):
        self.root = root
        root.title("Timer")
        root.config(bg = "Ghost White")
        
        self.playphoto = tk.PhotoImage(file = "C:\\Users\\judeh\\Downloads\\Play-Blue-Button-iconmini.png")
        self.pausephoto = tk.PhotoImage(file = "C:\\Users\\judeh\\Downloads\\Pause-Blue-Button-iconmini.png")
        self.refreshphoto = tk.PhotoImage(file = "C:\\Users\\judeh\\Downloads\\Button-Load-iconrefreshmini.png")
        self.savephoto = tk.PhotoImage(file = "C:\\Users\\judeh\\Downloads\\Button-Color-Circle-iconminisave.png")
        self.statsbutton = tk.PhotoImage(file = "C:\\Users\\judeh\\Downloads\\button_burn.png")
        
        self.state = False
        self.min = 20
        self.sec = 0
        
        self.minutes = 20
        self.seconds = 0
        
        self.meg = 0
        
        self.label = tk.Label(root, height=1, width=5,font = ("arial",55), textvariable="", activebackground="Ghost White")
        self.label.config(text = "ready?")
        self.label.grid(row=0, column=0, columnspan=4)
        
        self.button = tk.Button(root, image = self.playphoto, command = self.start_countdown)
        self.button.grid(row=1,column=0)
        
        self.pause_button = tk.Button(root, image = self.pausephoto, command = self.pause_countdown)
        self.pause_button.grid(row=1,column=1)
        
        self.stat_button = tk.Button(root, image = self.statsbutton, command = self.show_stat)
        self.stat_button.grid(row=1,column=3)
        
        self.save_button = tk.Button(root, image = self.savephoto, command = self.save)
        self.save_button.grid(row=1,column=2)
        
        self.graphic = tk.Label(root, text = "Tot: ", font = ("arial", 13))
        self.graphic.grid(row =2, column = 0, sticky = "w") 
        
        
        self.total = tk.Label(root, text = "", textvariable = "", font = ("arial", 13))
        self.label.config(text = self.meg)
        self.total.grid(row =2, column = 1) 
        
        
        #create database
        conn = sqlite3.connect('maaza.db')
        c = conn.cursor()
        c.execute("""CREATE TABLE IF NOT EXISTS lama (
            lemons  integer,    
            sqltime TIMESTAMP DEFAULT CURRENT_TIMESTAMP NOT NULL)
             """
             
      )

        conn.commit()
        conn.close()
        
   
    def countdown(self):
        #check to see if
        if self.state == True:
            if (self.min == 0) and (self.sec) == 0:
                self.label.config(text = "Fin")
                webbrowser.open("https://images.squarespace-cdn.com/content/v1/57ac397b6a4963c59357e09e/1525978609191-0FBH7GH8HQ7B8H5I7CF5/ke17ZwdGBToddI8pDm48kHfe_3QSjQG7tS_0wnIcW4dZw-zPPgdn4jUwVcJE1ZvWQUxwkmyExglNqGp0IvTJZUJFbgE-7XRK3dMEBRBhUpxm6yj5zwK48Gsn5r-0yw8F9uRHvPlOD6-bJJHh7ohpvpLj_Gf-r6ZPZsOXLvyin8Q/focusing-question.png")
                #below breaks out loop when paused
                self.state = False
                self.database()
                #kevin = "+20:00" + time.now()
                #self.listbox.insert(0, kevin)
                #happens whether or not you pause it
            else:
                #start countdown
                self.label.config(text="%02d:%02d" % (self.min, self.sec))
            
                #global instance
                #instance = lambda x, y: (self.min, self.sec)
                #instance = self.label.config(text="%02d:%02d" % (self.min, self.sec))
                #value = self.
                if self.sec == 0:
                    self.min -= 1
                    self.sec = 59
                else:
                    self.sec -=1
                    #print(self.minutes, self.seconds)
                    
                self.root.after(1000, self.countdown)
            
    def start_countdown(self):
        if self.state == False:
            self.state = True
            self.min = self.minutes
            self.sec = self.seconds
            self.countdown()
    def pause_countdown(self):
        if self.state == True:
            self.state = False
            #print(instance)
    def show_stat(self):
        popup = tk.Toplevel()
        popup.title("Question")
        
        
         
        #add scrollbar
        
        self.scrollbar = tk.Scrollbar(tk.TopLevel)
        self.scrollbar.config(command = self.listbox.yview)
        
        
        
        #add listbox
        self.listbox = tk.Listbox(tk.Toplevel, yscrollcommand = self.scrollbar.set, font = ('arial', '10', 'bold'), height = 10, width = 72)
        self.listbox.pack()
        
        
        
        
    def save(self):
       
        self.labeldown.config(text = "+ 10", font = ("arial", 13))
        self.labeldown.after(3000,self.labeldown.destroy)
    def wrap(self):
        self.meg = self.meg + 1200
        new = self.meg // 60 
        self.total.config(text = str(new) + "m")
    def database(self):
        conn = sqlite3.connect('maaza.db')
        c = conn.cursor()
        c.execute("INSERT INTO lama (lemons) VALUES (20)")
        conn.commit()
        conn.close()
        #print("added")
        self.wrap()
        
root = tk.Tk()
timer_instance_one = Timer(root)
if __name__ == '__main__':
    root.mainloop()
 
