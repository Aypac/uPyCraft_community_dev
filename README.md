# uPyCraft_src (community dev)
<b>uPyCraft is an IDE designed for micropython that supports Windows 7, 8, and 10, Linux, MAC OSX 10.11, and above.<br />
To make it easier for users, uPyCraft is released as standalone for all systems, so no need to install.</b>

This is a community clone, trying to give uPyCraft an urgently needed overhaul. This is not stable yet. Refer to <a href='https://github.com/DFRobot/uPyCraft_src'>the original github</a> for a stable version, but you are very welcome to contribute here (issues, pull releases, comments, testing).

The instructions below have not been checked recently and might be outdated. Generally, this project currently requires you to have python3.4, pyqt5, py2exe, QScintilla, pyserial and pyflakes installed.
<hr />

# Windows
## Installation
This requires you to have python3.4, pyqt5, py2exe, QScintilla, pyserial and pyflakes installed.

1. Python >=3.4:<br>

    Download from <a href="https://www.python.org/downloads/windows">the official website</a> <br>
        add python to the windows environment variable during installation.<br> 

    update pip： python -m pip install -U pip 
        add pip to the windows environment variable, such as C:/Python34/Scripts 
        
    pyserial:pip install pyserial 
    
    py2exe  : `pip install py2exe`
        Python34/Lib/site-packages/py2exe/icons.py Modify lines89:if iconheader.idCount>10 -> if iconheader.idCount>20
        
    pyflakes: `pip install pyflakes`
        find api.py and replace with pyflakesChange/api.py 
    
2. PyQt5:<br>
     You can simply install it with `pip install qscintilla PyQt5-tools serial pyserial`.

## Running
Open uPyCraft.py with python IDE, click the run module button/F5 to run.

## Package uPyCraft
uPyCraft.exe will be created in directory dist/ .


# Linux
## Environment
Ubuntu 16.04 LTS, Python >=3.5, PyQt5
## Install
### SIP<br>
Download SIP from https://riverbankcomputing.com/software/sip/download <br>

    tar zxvf sip-4.19.tar.gz -C /home/PyQt
    sudo python configure.py
    sudo make install
### QT support library<br>

    sudo apt-get install qt4-dev-tools qt4-doc qt4-qtconfig qt4-demos qt4-designer
    sudo apt-get install libqwt5-qt4 libqwt5-qt4-dev
### PyQt5<br>
Download PyQt4_gpl_x11-4.12 from https://sourceforge.net/projects/pyqt/files/PyQt4/ <br>

    tar zxvf PyQt4_gpl_x11-4.12.tar.gz -C /home/PyQt
    cd /home/PyQt/PyQt4_gpl_x11-4.12
    sudo python configure.py
    sudo make
    sudo make install
### QScintilla
Download QScintilla from https://sourceforge.net/projects/pyqt/files/QScintilla2/QScintilla-2.9.1/<br>

    `tar zxvf QScintilla-2.9.1.tar.gz`
    `cd QScintilla-2.9.1`
    #Qt4Qt5
    `cd Qt4Qt5`
    `qmake`
    `sudo make`
    `sudo make install`
    #Python
    `cd ../Python`
    `python3 configure.py`
    `sudo make`
    `sudo make install`
    #designer-Qt4Qt5
    `cd ../designer-Qt4Qt5`
    `qmake designer.pro`
    `sudo make`
    `sudo make install`
### Package uPyCraft<br>
    `pip install pyinstaller`
    pyinstaller -F uPyCraft.py
    
    
    
# Mac
## Environment
os 10.11 Python3.5 PyQt4
## Install
### qt4.8.7<br>
Download qt4.8.7 from http://mirrors.ustc.edu.cn/qtproject/archive/qt/4.8/4.8.7/qt-everywhere-opensource-src-4.8.7.tar.gz<br>

    cd Desktop
    tar vxf qt-everywhere-opensource-src-4.8.7.tar.gz
In qt-everywhere-opensource-src-4.8.7/src/gui/painting/qpaintengine_mac.cpp<br>
insted:
    
    CGColorSpaceRef colorSpace = 0;
    CMProfileRef displayProfile = 0;
    CMError err = CMGetProfileByAVID((CMDisplayIDType)displayID, &displayProfile);
    if (err == noErr) {
        colorSpace = CGColorSpaceCreateWithPlatformColorSpace(displayProfile);
        CMCloseProfile(displayProfile);
    }
to:

    CGColorSpaceRef colorSpace = CGDisplayCopyColorSpace(displayID);
    
install:

    cd qt-everywhere-opensource-src-4.8.7
    ./configure
    make  #2-4h
    sudo make install
    
configure environment:
    
    cd 
    vim .bash_profile
    
    PATH=/usr/local/Trolltech/Qt-4.8.7/bin:$PATH
    export PATH
    
    source ~/.bash_profile

qmake:
    
    qmake -v
    QMake version 2.01a
    Using Qt version 4.8.7 in /usr/local/Trolltech/Qt-4.8.7/lib
    
### SIP
Download SIP from https://sourceforge.net/projects/pyqt/files/sip/sip-4.19.8/sip-4.19.8.tar.gz/download<br>

    cd Desktop
    tar vxf sip-4.19.8.tar.gz
    cd sip-4.19.8
    sudo python3 configure.py
    sudo make install

### PyQt4
Download PyQt4 from https://sourceforge.net/projects/pyqt/files/PyQt4/PyQt-4.12.1/PyQt4_gpl_mac-4.12.1.tar.gz/download<br>

    cd Desktop
    tar vxf PyQt4_gpl_mac-4.12.1.tar.gz
    cd PyQt4_gpl_mac_4.12.1
    sudo python3 configure.py
    sudo make #20min
    sudo make install

### QScintilla
Download QScintilla from https://sourceforge.net/projects/pyqt/files/QScintilla2/QScintilla-2.9.1/QScintilla-gpl-2.9.1.tar.gz/download<br>

    cd Desktop
    tar vxf QScintilla-gpl-2.9.1.tar.gz
    cd QScintilla-gpl-2.9.1
    #Qt4Qt5
    cd Qt4Qt5
    qmake
    sudo make
    sudo make install
    #Python
    cd ../Python
    python3 configure.py
    sudo make
    sudo make install
    #designer-Qt4Qt5
    cd ../designer-Qt4Qt5
    qmake designer.pro
    sudo make
    sudo make install
    
### Package uPyCraft<br>

    pip install pyinstaller
    pyinstaller -F uPyCraft.py
    






