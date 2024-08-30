from json import loads
from requests import get
from turtle import Turtle,Screen,_Screen
from time import perf_counter as clock
from time import localtime,sleep
from tkinter import  Button, Pack
from tkinter.messagebox import askretrycancel,showinfo,showerror
from anmol import askinteger,askstring
from atexit import register,unregister
from random import choice
from configparser import ConfigParser
from screeninfo import get_monitors
from sys import exit

#Base variables
App_Name="TFOC"
version=1.2
patch_available=False
a=get_monitors()
height=a[0].height
width=a[0].width
var_list={'player_whsID':0,'friendID_list':[ ],'font':"Courier New",'text_color':"White",'bgcolor':"Black",'writing_speed':5}

del get_monitors

#Exiting function
def exit_f():
    from turtle import Terminator
    global player_whsID
    global friendID_list
    global font
    global text_color
    global bgcolor
    global writing_speed
    global new_config
    global config
    
    for i in var_list:
        new_config['Engine'][i]=str(eval(i))
    if new_config!=config:
        config_file=open('./../Config/TransEngine.ini','w')
        new_config.write(config_file)
        config_file.close()
        logger('Config: Changes detected into app configuration\n')
        logger('Config: Successfully updated config file\n')
    a=Terminator()
    logger('Exit: Exit requested\n')
    logger('Exit: GUI/Window shut down\n')
    logger('Exit: Modules shut down\n')
    logger('Exit: Preparing to Exit\n')
    logger("Exit: Logging Closed Successfully for 'Transformers Fall Of Cybertron Statistics' application\n")
    log.close()

register(exit_f)

#Important functions
#=====================================================================================================================================================================================
def update_exe():
    from turtle import Terminator
    global version
    global Latest_version
    t.clear()
    t.write(f'Updating to {Latest_version}',font=(font,15))
    logger(f'Updating to {Latest_version}\n')

    a=get(f"https://raw.githubusercontent.com/AnmolBhaiyaShah/data/main/{App_Name}/FOC_Stats.exe")
    a=a.content
    b=open('./FOC_Stats.exe','wb')
    b.write(a)
    b.close()

    a=Terminator()
    t.clear()
    t.write('Successfully updated,restart the program for new changes',font=(font,15))
    logger(f'Successfully updated from {version} -> {Latest_version}\n')
    logger("Exit: Logging Closed Successfully for 'Transformers Fall Of Cybertron Statistics' application\n")
    log.close()

def date(localtime):
    d=str(f"{localtime[1]:02}")+'/'+str(f"{localtime[2]:02}")+'/'+str(f"{localtime[0]:02}")
    return d

def time():
    lt=localtime()
    d=date(lt)
    t=str(f"{lt[3]:02}")+':'+str(f"{lt[4]:02}")+':'+str(f"{lt[5]:02}")
    ct='['+d+' '+t+'] '
    return ct
def logger(n):
    ct=str(time())
    log.write(ct)
    if '\n' not in n:
        n=n+'\n'
    log.write(n)
    log.flush()

def enc_dec(text,operation=str):
    if operation=='decode':
        a=text
        for i in encoding_schemes[::-1]:
            a=eval(operation+'(a,i)')
        return a
    else:
        a=text
        for i in encoding_schemes:
            a=eval(operation+'(a,i)')
        return a

def font_installed(font_name):
    from matplotlib.font_manager import fontManager
    font_names = [f.name for f in fontManager.ttflist]
    del fontManager
    return font_name in font_names

def verify_whs_id(name):
    try:
        a=get('https://api.aiwarehouse.xyz/foc/data/whs_id?whs_usernames='+name)
        a=loads(a.text)
        ID=a['data'][name]
        logger('Log: Successfully verified user '+name+' with ID='+str(ID)+'\n')
        return ID
    except:
        log('Error: Verification failed with Error: Connection error\n')
        showerror('Internet Error','Could not make a connection')
    

def update_name():
    global player_whsID
    global player_name
    user_input=askstring('Update user name','Use a TFOC username','./../CookedPC/Icon.xxx',initialvalue=player_name)
    if user_input!=None:
        ID=verify_whs_id(user_input)
        if ID!=0:
            player_whsID=ID
            showinfo('Name changed','Successfully updated name to ☑'+user_input+'\nRefresh/Restart for changes to take effect')
        else:
            showerror('Invalid!','Entered username is invalid')

def update_friend_list():
    user_input=askstring('Update your Friend list','Add a TFOC friend to your friend list','./../CookedPC/Icon.xxx')
    if user_input!=None:
        ID=verify_whs_id(user_input)
        if ID!=0:
            global friendID_list
            friendID_list.append(ID)
            showinfo('Friend Added','Successfully added ☑'+user_input+' To your friend list'+'!\n'+'Refresh/Restart for changes to take effect')
        else:
            showerror('Invalid!','Entered username is invalid')

def update_font():
    global font
    user_input=askstring('Change Font','Change the font used by this application','./../CookedPC/data_2.dat',initialvalue=font)
    if user_input!=None:
        if font_installed(user_input):
            font=user_input
            showinfo('Font changed','Successfully changed font to '+font+'!\n''Refresh/Restart for changes to take effect\nThis will work only if the said font is \ninstalled otherwise it will switch to default')
        else:
            showerror('Font Not found!','Entered font is either not installed or you made a typo in the name')

def update_text_color():
    global text_color
    user_input=askstring('Change text color','Change text color using a valid color name','./../CookedPC/data_2.dat',initialvalue=text_color)
    try:
        if user_input!=None:
            text_color=user_input
            t.color(text_color)
            showinfo('Text color changed','Successfully changed text color to '+text_color+'\nRefresh/Restart for changes to take effect')
    except:
        showerror('Text color change failed','Invalid color name: '+text_color+'\nPlease retry.')

def update_bgcolor():
    global bgcolor
    user_input=askstring('Change background color','Change background color using a valid color name','./../CookedPC/data_2.dat',initialvalue=bgcolor)
    try:
        if user_input!=None:
            bgcolor=user_input
            T.bgcolor(bgcolor)
            showinfo('Background color changed','Successfully changed background color to '+bgcolor+'\nRefresh/Restart for changes to take effect')
    except:
        showerror('Background color change failed','Invalid color name: '+bgcolor+'\nPlease retry.')

def update_writing_speed():
    global writing_speed
    user_input=askinteger('Change writing speed','Change writing speed using a valid integer','./../CookedPC/data_2.dat',initialvalue=writing_speed)
    if user_input!=None:
        writing_speed=user_input
        t.speed(writing_speed)
        showinfo('Writing speed changed','Successfully changed writing speed to '+str(writing_speed)+'\nRefresh/Restart for changes to take effect')

#=====================================================================================================================================================================================

#Logging started
log=open('./../Logs/log.txt','w')
logger("Init: Logging Started Successfully for 'Transformers Fall Of Cybertron Statistics' application\n")


try:
    #Look for config and error
    a=None
    b=None
    c=None
    #Read config
    try:
        logger('Config: Initalizing config file\n')
        config_open=open('./../Config/TransEngine.ini','r')
        logger('Config: Config file check status :  Found\n')
        config_open.close()
        pass
    except:
        logger('Error : Config file check status : Error : Missing\n')
        config_w=open('./../Config/TransEngine.ini','w')
        a=get(f"https://raw.githubusercontent.com/AnmolBhaiyaShah/data/main/{App_Name}/TransEngine")
        b=(a.content).decode('utf-8')
        config_w.write(b)
        config_w.close()
        logger('Config: Config file damaged or missing, redownloading from server\n')
        
    #Global Variables
    config         =ConfigParser()
    new_config     =ConfigParser()
    config.read    ('./../Config/TransEngine.ini')
    new_config.read('./../Config/TransEngine.ini')
    logger('Init: Initializing variables\n')

    #Config vars processor
    for i in var_list:
        try:
            try:
                a=eval(config['Engine'][i].strip())
            except:
                a=(config['Engine'][i].strip())
            logger("Init:    "+i+'='+str(a)+'\n')
        except:
            a=var_list[i]
            logger('Error:    Missing variable TransEngine.ini/'+i+'; continuing with '+i+'='+str(a)+'\n')
        exec(i+"=a")
    logger('Config: Config initialized\n')

    #Window setup
    window_width_ratio     =1.0
    window_height_ratio    =1.0
    header_font_size=10
    data_font_size  =10

    #Text location deviation
    d_deviator=0
    if data_font_size>10 and data_font_size<15:
        d_deviator=3
    elif data_font_size>15 and data_font_size<20:
        d_deviator=5
    data_font_deviation=0
    #-----------------------------------------------------------------------
    #GUI
    logger('Init: Initializing GUI/Window\n')
    T = Screen()
    T.setup(width=window_width_ratio, height=window_height_ratio) # Note that it needs to be 1.0, and not 1
    t =Turtle()
    t.color(text_color)
    t.up()
    t.hideturtle()
    t.speed(writing_speed)
    try:
        _Screen()._root.iconbitmap('./../CookedPC/Icon.xxx')
    except:
        logger('Window : Icon file not found, redownloading icon from server\n')
        a=get(f"https://raw.githubusercontent.com/AnmolBhaiyaShah/data/main/{App_Name}/Icon_D.xxx")
        b=a.content
        data_w=open('./../CookedPC/Icon.xxx','wb')
        data_w.write(b)
        data_w.close()
        _Screen()._root.iconbitmap('./../CookedPC/Icon.xxx')
        logger('Window : File downloaded successfully!\n')
    T.bgcolor(bgcolor)
    T.title(f"Transformers Fall Of Cybertron Statistics  - {version}")
    logger('Init: GUI/Window initialized\n')

    #Font deviation
    header_font_size=int(((width/1920)*header_font_size)//1)
    data_font_size=  int((((width/1920))*data_font_size)//1)
    #-----------------------------------------------------------------------

    #Register online
    t.setpos(int(width/1920*(-100)),0)
    t.write('Initializing....',font=(font,15))
    
    def foc():
        global a
        global b
        global c
        global patch_available
        global player_name
        global Latest_version

        if player_whsID!=0:
            url="https://api.aiwarehouse.xyz/foc/data/whs_username?whs_ids="+str(player_whsID)
            a=get(url)
            a=loads(a.text)
            player_name=a['data'][str(player_whsID)]
        else:
            player_name='Default'

        #github server
        if True:
            logger('DevNet: Connecting to server side data....\n')
            t.clear()
            t.setpos(int(width/1920*(-200)),-50)
            t.write('Connecting to server....',font=(font,15))
            b = get(f"https://raw.githubusercontent.com/AnmolBhaiyaShah/data/main/{App_Name}/TransDictionary")
            k=eval(b.content)
            t.clear()
            t.write('Connection Successful!....',font=(font,15))
            
            force_motd=k['force motd']
            dm_disabled=k['dm_disabled']
            Latest_version=k['Latest version']
            Announcement=k['Announcement']
            Force_permanent_announcement=k['Force_permanent_announcement']

            if Latest_version>version:
                patch_available=True
            else:
                patch_available=False

            if force_motd.strip() != '':
                motd=force_motd
            else:
                motd=k['motd']
                motd=choice(motd)

            logger('DevNet: Data recieved successfully!\n')
        t.clear()
        logger('Init: Initalizing recieved data\n')

        if patch_available:
            unregister(exit_f)
            register(update_exe)
            exit()

        #-----Announcements-----
        #Perma_Announcement
        if Force_permanent_announcement.strip() != '':
            x_pos=-int(((len(Force_permanent_announcement)/2)//1)*(header_font_size*1.3)//1)
            t.setpos(x_pos,0)
            t.write(Force_permanent_announcement,font=(font,15))
            exit()
        else:
            pass
        #Temp_announcement
        if Announcement.strip() != '':
            x_pos=-int(((len(Announcement)/2)//1)*(header_font_size*1.3)//1)
            t.setpos(x_pos,0)
            t.write(Announcement,font=(font,15))
            sleep(5)

        else:
            pass

        #Main site URL
        url="https://api.aiwarehouse.xyz/18341/sessions"

        #Website data processing
        msg='DevNet: Lookup started for server ' + str(url)+'\n'
        logger(msg)
        try:
            a_get=get(url)
            logger('DevNet: Response recieved from foc servers\n')
            pass
        except:
            logger('DevNet: Error connecting to server, likely an internet connection issue\n')
            while True:
                b=askretrycancel('No Internet connection','Try Again?')
                if b==True:
                    try:
                        a_get=get(url)
                        logger('Response recieved from FOC servers\n')
                        pass
                    except:
                        continue
                if b==False:
                    logger('Exit: Application exited successfully with exit code : No internet\n')
                    log.close()
                    break
                    exit()
        #Process
        while True:
            if '{"error":false,"message":null,"data":' in str(a_get.text):
                c=loads(a_get.text)
                break
            else:
                a_get=get(url)
        at=clock()

        logger('Init: Initalizing recieved data\n')
        t.clear()
        k=c
        length=len(k["data"])

        #=================================================================
        online_friends=[]
        online_users=[]
        hex_user_data={}
        gamemode_wise_data={}
        online_users=[]
        user_gamemode_visibility=[]
        url='https://api.aiwarehouse.xyz/foc/data/whs_username?whs_ids='

        t.clear()
        t.setpos(int(width/1920*(-120)),0)
        t.write('Processing Received data',font=(font,15))

        #Analyzing processed data
        c=['NULL','DM','TDM','HH','CTF','ESC','Menu/Party Lobby','Conquet',]
        games=[0,0,0,0,0,0,0,0]

        #Session data
        for i in range(0,length):
            usernames=int (k['data'][i]['session_payload']['host_username'],16)
            gamemode=      k['data'][i]['session_payload']['game_type']
            private_flag=  k['data'][i]['session_payload']['private_flag']

            if private_flag==0:
                private_flag='Public'
            else:
                private_flag='Private'

            gamemode=c[gamemode]
            user_gamemode_visibility=[gamemode,private_flag]

            if usernames in hex_user_data:
                if gamemode!=c[6]:
                    user_gamemode_visibility=[gamemode,private_flag]
                if gamemode==c[6]:
                    continue
            hex_user_data[usernames]=user_gamemode_visibility
            url+=str(usernames)+','

        a = get(url)
        b=loads(a.text)

        for i in hex_user_data:
            usernames=b['data'][str(i)]
            gamemode_wise_data[usernames]=hex_user_data[i]
            online_users.append(usernames)

            #Friends info
            if i in friendID_list:
                if usernames not in online_friends:
                    online_friends.append(usernames)

        #Gamemodes
        del hex_user_data
        for i in gamemode_wise_data:
            gamemode=gamemode_wise_data[i][0]
            index=c.index(gamemode)
            games[index]+=1

        dm   =str(games[1])
        tdm  =str(games[2])
        hh   =str(games[3])
        ctf  =str(games[4])
        esc  =str(games[5])
        menu =str(games[6])
        dom  =str(games[7])

        output=open('./output.txt','w')
        output.write(str(online_users)+'\n'+str(gamemode_wise_data))
        output.close()
        gamemode_wise_data=str(gamemode_wise_data)[1:-1]

        #turtle window
        logger('Log: Writing processed data on window\n')
        try:
            t.clear()
                
            t.speed(99999)
            x_pos=int(width/1920*(400))
            y_pos=int(height/1080*(-450))
            t.setpos(x_pos,y_pos)
            t.write('Made By @anmolbhaiyashah',font=(font,header_font_size))
            x_pos=int(width/1920*(-790))
            y_pos=int(height/1080*(-450))
            t.setpos(x_pos,y_pos)
            t.write('Player Name                 : ',font=(font,header_font_size))
            x_pos=int(width/1920*(-490))
            y_pos=int(height/1080*(-450))
            t.setpos(x_pos,y_pos)
            t.write(player_name,font=(font,header_font_size))
            
            t.speed(writing_speed)
            x_pos=-int(((len(motd)/2)//1)*header_font_size)
            t.setpos(x_pos,400)
            t.write(motd,font=(font,header_font_size))
            x_pos    =int(width/1920*(-790))
            y_pos    =int(height/1080*(350))
            t.setpos(x_pos,y_pos)
            t.write("TDM players                 : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos)
            t.write(tdm,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-35)
            t.write("ESC players                 : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-35)
            t.write(esc,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-70)
            t.write("DeathMatch players          : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-70)
            if dm_disabled:
                t.write('DeathMatch mode has been disabled in the recent patch',font=(font,header_font_size))
            else:
                t.write(dm,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-105)
            t.write("Conquest players            : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-105)
            t.write(dom,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-140)
            t.write("Capture The Flag players    : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-140)
            t.write(ctf,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-175)
            t.write("Head Hunter players         : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-175)
            t.write(hh,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-210)
            t.write("MP/ESC Party Lobby          : ",font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-210)
            t.write(menu,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-245)
            t.write('Online friends              : ',font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-245)
            t.write(online_friends,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-280)
            t.write('Total online friends        : ',font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-280)
            t.write(len(online_friends),font=(font,data_font_size))
            t.setpos(x_pos,y_pos-315)
            t.write('Online users                :',font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-315)
            t.write(online_users,font=(font,data_font_size))
            t.setpos(x_pos,y_pos-350)
            t.write('Total online users          :',font=(font,header_font_size))
            t.setpos(x_pos+300+data_font_deviation,y_pos-350)
            t.write(len(online_users),font=(font,data_font_size))
            t.setpos(x_pos,y_pos-385)
            t.write('Gamemode Wise Data          :',font=(font,header_font_size))
            c=y_pos-385
            n=int((height/1080)*(145))
            if len(gamemode_wise_data)>0:
                for i in range(0,len(gamemode_wise_data),n):
                   b=gamemode_wise_data[i:i+n]
                   t.setpos(x_pos+300+data_font_deviation,c)
                   t.write(b,font=(font,data_font_size))
                   c=c-30
            else:
                t.setpos(x_pos+300+data_font_deviation,c)
                t.write('No online Player',font=(font,data_font_size))
            if patch_available==True:
                t.setpos(int(width/1920*(400)),int(height/1080*(320)))
                t.write("Patch Available!",font=(font,header_font_size))
            t.setpos(int(width/1920*(400)),int(height/1080*(290)))
            t.write("Version  : "+str(version),font=(font,header_font_size))
            t.setpos(int(width/1920*(700)),int(height/1080*(290)))
            if player_name in online_users:
                t.setpos(x_pos,int(height/1080*(-420)))
                t.write("If you don't already know this, then know that you are playing Transformers Fall Of Cybertron",font=(font,data_font_size))
            logger('Log: Finished writing on window\n')
        except:
            exit()

        #clock end
        try:
            et = clock()
            msg="Runtime: %.2f sec." % (et-at)
            t.setpos(int(width/1920*(400)),int(height/1080*(260)))
            t.write(msg,font=(font,header_font_size))
        except:
            exit()
    foc()
    
    #Buttons setup
    button_name           = Button(None, {'text': 'Change Player name ','command':update_name,'cursor':'hand2',Pack:{'side':'left'}})
    button_friendlist     = Button(None, {'text': 'Update Friend list','command':update_friend_list,'cursor':'hand2',Pack:{'side':'left'}})
    button_font           = Button(None, {'text': 'Change App Font','command':update_font,'cursor':'hand2',Pack:{'side':'left'}})
    button_text_color     = Button(None, {'text': 'Change Text color','command':update_text_color,'cursor':'hand2',Pack:{'side':'right'}})
    button_bgcolor        = Button(None, {'text': 'Change BG Color','command':update_bgcolor,'cursor':'hand2',Pack:{'side':'right'}})
    button_writing_speed  = Button(None, {'text': 'Change writing speed','command':update_writing_speed,'cursor':'hand2',Pack:{'side':'right'}})
    button_refresh        = Button(None, {'text': 'Refresh','command': foc,'cursor':'hand2',Pack: {}})
    button_refresh.mainloop()

except:
    exit()
