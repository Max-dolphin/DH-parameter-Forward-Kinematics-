# DH-parameter-Forward-Kinematics-
# Direct/Forward kinemayics of robot.
import numpy as np
print ('**Compution of Forward Kinematics**')
frame= int(input('Enter total number of frame :'))

# Value of the base frame.
finalf =np.array([[1.0,0,0,0],[0,1.0,0,0],[0,0,1.0,0],[0,0,0,1.0]])

# For interested amount of frame.
for i in range (1,frame+1):
	print ('\nFor Frame',i)

# Enter the values by computing and by D-H parameter.
	jointa =float(input('  Enter joint angle (θ) :'))
	offset =float(input('  Enter offset (d) :'))
	twista =float(input('  Enter twist angle (α) :'))
	lenolk=float(input('  Enter length of the link angle (a) :'))

# Converting angle degree to angle radian.
	jointa=(jointa/180.0)*np.pi
	twista=(twista/180.0)*np.pi

# Creating Z-Screw matrix.
	zrot=np.array([[np.cos(jointa),-np.sin(jointa),0,0],[np.sin(jointa),np.cos(jointa),0,0],[0,0,1,0],[0,0,0,1]])
	ztrans=np.array([[1,0,0,0],[0,1,0,0],[0,0,1,offset],[0,0,0,1]])
	tz=np.dot(zrot,ztrans)

# Creating X-Screw matrix.
	xrot=np.array([[1,0,0,0],[0,np.cos(twista),-np.sin(twista),0],[0,np.sin(twista),np.cos(twista),0],[0,0,0,1]])
	xtrans=np.array([[1,0,0,lenolk],[0,1,0,0],[0,0,1,0],[0,0,0,1]])
	tx=np.dot(xrot,xtrans)

# Matrix multiplication of Z-screw and X-screw matrix.
	tzx=np.dot(tz,tx)
	
#Displaying multiplied matrix.
	print ('The rotation of frame', i ,'with respect to frame',i-1,':\n',tzx)

#Multiplying all frame matrix and displaying.
	finalf=np.dot(finalf,tzx)
print ('\n\nThe rotation of frame',frame,'with respect to frame 0 :\n',finalf)
