#DESIGN OF SYNCHRONOUS COUNTERS
#DONE BY - THIRAVIDASELVI(2019105063)

"""
AIM: To derive the logical expressions for the inputs to the flip-flops(JK or D or T)
     in a synchronous counter.

DESCRIPTION: Given the type of flip-flop to be used and the sequence in which the
             synchronous counter should count, the program displays the logical
             expression(s) for the input(s) to each of the flip-flops by using the
             state transition table which makes use of the excitation table and the
             simplication of boolean expression using Quine McCluskey Algorithm.

NOTE: The maximum value that can be counted as a state is 15 i.e., the maximum number of
      flip-flops(bits) is 4. The flip-flop displayed first corresponds to the LSB and the
      flip-flop displayed last corresponds to the MSB.
      The variables for the number of bits are indicated as follows:
      (leftmost=MSB;rightmost=LSB)
      2 Bits - AB
      3 Bits - ABC
      4 Bits - ABCD
"""

def zeros(m):           #GENERATES 'm' ZEROS
    a=''
    for i in range(m):
        a+='0'
    return a

def ABCD(str_f):        #RETURNS THE MINTERMS TO BE PRINTED
        str_f1=""
        str_f2=""
        if(str_f=="" or str_f=="+" or str_f=="++" or str_f=="+++"):
            return('1')
        if(str_f[0]=="+" and (str_f[1]=="w" or str_f[1]=="x" or str_f[1]=="y" or str_f[1]=="z")):
            str_f1=str_f[1:]
        else:
            str_f1=str_f
        for i in range(0,len(str_f1)):
            if(str_f1[i]=='w'):
                str_f2+='A'
            elif(str_f1[i]=='x'):
                str_f2+='B'
            elif(str_f1[i]=='y'):
                str_f2+='C'
            elif(str_f1[i]=='z'):
                str_f2+='D'
            else:
                str_f2+=str_f1[i]
        return(str_f2)
    
def j_k_ff(p):          #DESIGN USING JK FLIP FLOP
        j_0=[]
        j_1=[]
        j_d=[]
        k_0=[]
        k_1=[]
        k_d=[]
        for i in range(p,m*n,m):
            if ((q1_str[i]=='0') and (q2_str[i]=='0')):
                j_0.append(int(q_t1[i//m],2))
                k_d.append(int(q_t1[i//m],2))
            elif ((q1_str[i]=='0') and (q2_str[i]=='1')):
                j_1.append(int(q_t1[i//m],2))
                k_d.append(int(q_t1[i//m],2))
            elif ((q1_str[i]=='1') and (q2_str[i]=='0')):
                j_d.append(int(q_t1[i//m],2))
                k_1.append(int(q_t1[i//m],2))
            else:
                j_d.append(int(q_t1[i//m],2))
                k_0.append(int(q_t1[i//m],2))
        for i in all_states:
                if (i not in (j_0+j_1+j_d)):
                        j_d.append(i)
                        k_d.append(i)
        print("\nFlip Flop",m-p,":")
        j_f=minFunc(m,'('+str(j_1)+')d('+str(j_d)+')')
        k_f=minFunc(m,'('+str(k_1)+')d('+str(k_d)+')')
        print("\nj =",ABCD(j_f))
        print("k =",ABCD(k_f))

def d_ff(p):            #DESIGN USING D FLIP FLOP
        d_0=[]
        d_1=[]
        d_d=[]
        for i in range(p,m*n,m):
                if (q2_str[i]=='1'):
                        d_1.append(int(q_t1[i//m],2))
                else:
                        d_0.append(int(q_t1[i//m],2))
        for i in all_states:
                if (i not in (d_0+d_1)):
                        d_d.append(i)
        print("\nFlip Flop",m-p,":")
        d_f=minFunc(m,'('+str(d_1)+')d('+str(d_d)+')')
        print("\nd =",ABCD(d_f))

def t_ff(p):            #DESIGN USING T FLIP FLOP
        t_0=[]
        t_1=[]
        t_d=[]
        for i in range(p,m*n,m):
            if (q1_str[i]!= q2_str[i]):
                t_1.append(int(q_t1[i//m],2))
            else:
                t_0.append(int(q_t1[i//m],2))
        for i in all_states:
                if (i not in (t_0+t_1)):
                        t_d.append(i)
        print("\nFlip Flop",m-p,":")
        t_f=minFunc(m,'('+str(t_1)+')d('+str(t_d)+')')
        print("\nt =",ABCD(t_f))


def minFunc(numVar, stringIn):      # K-Map Minimization
	num= int(numVar)
	x= stringIn
	l= []
	i=0
	while(x[i]!='d'):
		if(x[i].isdigit()==True):                       # taking the values from the input, and storing it in a list
			if(x[i+1].isdigit()==False):
				l.append(x[i])
				i+=1
			else:
				l.append(x[i]+x[i+1])
				i+=2
		else:
			i+=1
		y=i
	ess=list(l)                                             #storing essential prime implicant in a seprate list for further use
	if(x[y+1]!='-'):
		while(x[y]!=')'):
			if(x[y].isdigit()==True):
				if(x[y+1].isdigit()==False):    #storing the dont care condition giving in the input
					l.append(x[y])
					y+=1
				else:
					l.append(x[y]+x[y+1])
					y+=2
			else:
				y+=1
	if(num==4):
		for i in range(len(l)):				#converting to binary for 4 variables
			l[i] = format(int(l[i]), '04b')
	elif(num==3):
		for i in range(len(l)):		         	#converting to binary for 3 variables
			l[i] = format(int(l[i]), '03b')
	elif(num==2):
		for i in range(len(l)):				#converting to binary for 2 variables
			l[i] = format(int(l[i]), '02b')

	a,b,c,d,e,f,g,h,p,q,w,r,t,y,m,n,o,z,u,v = [],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[]  	
	l.sort()
	count = 0
	t=0

	#  Quine-McCluskey and Petrick methods - 

	for i in range(len(l)):
			for j in range(num):				#Storing the digit speratly on the basis of much many 1's they contain
				if(l[i][j]=='1'):
					count+=1
			if(count==0):
				a.append(l[i])
			if(count==1):					#appending into one of the list created above for seperation
				b.append(l[i])
			if(count==2):
				c.append(l[i])
			if(count==3):
				d.append(l[i])
			if(count==4):
				e.append(l[i])
			count=0

	def step1(a,b,f):  						# Proceding tp step 1 comparing a and b then follows on uptil all thrr couples are compared 
		count=0
		for i in range(len(a)):
			for k in range(len(b)): 		    
				for j in range(num):
					if(a[i][j]!=b[k][j]):
						count+=1
				if(count==1):
					for j in range(num):
						if(a[i][j]!=b[k][j]):
							f.append(str(str(a[i][:j])+'x'+str(a[i][j+1:])+',('+str(int(a[i],2))+','+str(int(b[k],2))+')'))    
				count=0
		return(f)

	f=step1(a,b,f)					
	g=step1(b,c,g)
	h=step1(c,d,h)
	p=step1(d,e,p)

	def step2(f,g,q):
		count=0
		for i in range(len(f)): 		#same as step 1 , step 2 does the same on the output of step 1 and give us a compariable impicants
			for k in range(len(g)):
				for j in range(num):
					if(f[i][j]!=g[k][j]):			
						count+=1
				if(count==1):
					for j in range(num):
						if(f[i][j]!=g[k][j]):
							q.append(str(str(f[i][:j])+'x'+str(f[i][j+1:-1])+','+ str(g[k][num+2:])))   
				count=0
		return(q)

	q = step2(f,g,q)                                
	w = step2(g,h,w)
	r = step2(h,p,r)

	def step3(f,g,q):
		count=0
		for i in range(len(f)):			#same as step 2 , step 3 does the same on the output of step 2 and give us a compariable impicants
			for k in range(len(g)):
				for j in range(num):
					if(f[i][j]!=g[k][j]):
						count+=1				
				if(count==1):
					for j in range(num):
						if(f[i][j]!=g[k][j]):
							q.append(str(str(f[i][:j])+'x'+str(f[i][j+1:-1])+ ',' +str(g[k][6:]))) 		
				count=0
		return(q)
	m = step3(q,w,m)			                
	n = step3(w,r,n)

	def step4(f,g,p):
		count=0
		for i in range(len(f)):			#same as step 3 , step 4 does the same on the output of step 3 and give us a compariable impicants
			for k in range(len(g)):
				for j in range(num):
					if(f[i][j]=='x'):			
						if(g[k][j]=='x'):
							count+=1
				if(count==2):
					for j in range(num):
						if(f[i][j]!=g[k][j]):
							p.append(str(str(f[i][:j])+'x'+str(f[i][j+1:-1])+ str(g[k][-4:])))  
				count=0
		return(p)				
	o = step4(m,n,o)		    

	z=list(o)
	if(len(z)==0):
		z=list(m)
		z.extend(n)	 			# getting the last unempty ist so that we can have the prime implicants stored in a particular list
	if(len(z)==0):
		z=list(q)
		z.extend(w)
		z.extend(r)
	if(len(z)==0):
		z=list(f)
		z.extend(g)
		z.extend(h)
		z.extend(p)
	if(len(z)==0):
		z=list(a)
		z.extend(b)
		z.extend(c)
		z.extend(d)
		z.extend(e)

	def concatinate(q):				#concatinating the list of unneccesary repeatation of the implicants
		for i in range(len(q)):
			for k in range(1+i,len(q)):
				if(q[i][:num]==q[k][:num]):
					q[k] = ''
		while '' in q:
			q.remove('')
		return(q)					

	z = concatinate(z)  

	if ")" in z[0]:		
		def left(q):				#getting whats left in quine method of table and storing it in another list
			for i in range(len(q)):
				j=num+1
				while(q[i][j]!=')'):
					if(q[i][j].isdigit()==True):
						if(q[i][j+1].isdigit()==False):
							u.append(q[i][j])
							j+=1
						else:
							u.append(q[i][j]+q[i][j+1])
							j+=2
					else:
						j+=1
			return(u)						
		u=left(z)								

		def simple(u):				#removing repeated entries
			for i in range (len(u)):
				for k in range(i+1,len(u)):
					if(u[i]==u[k]):
						u[k]=''
			while '' in u:
				u.remove('')
			return(u)			
		u=simple(u)					


	# Further code deals with the dont care conditions 

		def dcare(f,u,v):
			count=0
			for i in range(len(f)):
				j=5		        #to find out whats left, for loop run all over
				while(f[i][j]!=')'):
					if(f[i][j].isdigit()==True):
						if(f[i][j+1].isdigit()==False):
							if(f[i][j] not in u):
								count+=1							
								u.append(f[i][j])
							j+=1
						else:
							if(f[i][j]+f[i][j+1] not in u):
								count+=1
								u.append(f[i][j]+f[i][j+1])
							j+=2
					else:												
						j+=1
				if(count>=1):
					v.append(f[i])
				count=0
			return(v,u)

		def acare(a,b,c,d,e,v):
			if(len(a)==0 and len(c)==0):
				v.extend(b)	        #checking the left over in the very first seperation table
			if(len(b)==0 and len(d)==0):
				v.extend(c)
			if(len(c)==0 and len(e)==0):
				v.extend(d)
			if(len(d)==0):
				v.extend(e)
			for i in range(len(v)):
				v[i]=str(int(v[i],2))	#converting to decimal in returning the value
			return(v)
		v=acare(a,b,c,d,e,v)
		v,u=dcare(n,u,v)
		v,u=dcare(m,u,v)
		v,u=dcare(r,u,v)			#checking each step of the quine table for left over elements
		v,u=dcare(w,u,v)
		v,u=dcare(q,u,v)
		v,u=dcare(p,u,v)
		v,u=dcare(h,u,v)
		v,u=dcare(g,u,v)
		v,u=dcare(f,u,v)
		v=concatinate(v)

		z.extend(v)	
                                                        #storing all implicants including dont care in the same list
		def order(z):
			for i in range(len(z)):
				count=0
				count1=0
				for j in range(num):
					if(z[i][j]=='x'):
						count1+=1
				a=num+1
				while(z[i][a]!=')'):
					if(z[i][a].isdigit()==True):
						if(z[i][a+1].isdigit()==False):
							if z[i][a] in ess:
								count+=1
							a+=1
						else:
							if((z[i][a]+z[i][a+1]) in ess):
								count+=1
							a+=2
					else:
						a+=1
				if(count==(2*count1)):
					temp = z[0]
					z[0]=z[i]
					z.pop(i)
					z.insert(1,temp)
			return(z)
		z=order(z)

		def imp(z):
			prime=[]
			for i in range(len(z)):
				count=0
				j=num+1
				while(z[i][j]!=')'):
					if(z[i][j].isdigit()==True):
						if(z[i][j+1].isdigit()==False):
							if z[i][j] in ess:
								count+=1
								ess.remove(z[i][j])
							j+=1
						else:
							if((z[i][j]+z[i][j+1]) in ess):
								count+=1
								ess.remove((z[i][j]+z[i][j+1]))
							j+=2
					else:
						j+=1
				if(count>=1):
					prime.append(z[i])
			return(prime)
		z=imp(z)

	# Expresing the prime implicants in the form of 4 variables

	def exp(z):
		if(num==4):
			dir = {0:'abcd',1:'abcz',2:'abyd',3:'abyz',4:'axcd',5:'axcz',6:'axyd',7:'axyz',8:'wbcd',9:'wbcz',10:'wbyd',11:'wbyz',12:'wxcd',13:'wxcz',14:'wxyd',15:'wxyz'}
		elif(num==3):
			dir = {0:'abc',1:'aby',2: 'axc',3:'axy',4:'wbc',5:'wby',6:'wxc',7:'wxy'}		
		elif(num==2):
			dir = {0:'ab',1:'ax',2: 'wb',3:'wx'}
		f=''
		if ')' in z[0]:
			for i in range(len(z)):
				s=[]								
				j=num+1
				while(z[i][j]!=')'):
					if(z[i][j].isdigit()==True):
						if(z[i][j+1].isdigit()==False):
							s.append(dir[int(z[i][j])])				
							j+=1
						else:
							s.append(dir[int(z[i][j]+z[i][j+1])])
							j+=2
					else:
						j+=1
				for j in range(num):
					count=0
					for k in range(0,len(s)-1):
						if(s[k][j]==s[k+1][j]):				
							count+=1
					if(count==(len(s)-1)):
						if(s[k][j]=='a'):
							f=f+'w\''
						elif(s[k][j]=='b'):
							f=f+'x\''
						elif(s[k][j]=='c'):
							f=f+'y\''
						elif(s[k][j]=='d'):
							f=f+'z\''
						else:
							f=f+s[k][j]
				if(i!=(len(z)-1)):
					f=f+'+'		
		else:
			s=[]
			decimal =0
			for i in range(len(z)):
				for digit in z[i]:
					decimal = decimal*2 + int(digit)	
				z[i]=decimal
				decimal=0
			for i in range(len(z)):
				s.append(dir[(z[i])])
			for i in range(len(s)):
				for j in range(len(s[i])):
					if(s[i][j]=='a'):
							f=f+'w\''
					elif(s[i][j]=='b'):
						f=f+'x\''
					elif(s[i][j]=='c'):
						f=f+'y\''
					elif(s[i][j]=='d'):
						f=f+'z\''
					else:
						f=f+s[i][j]
				if(i!=(len(z)-1)):
					f=f+'+'		    #SOP operator
		return(f)
	stringOut=exp(z)		
	return (stringOut)    	                            #returning the K map value back
 
#PROGRAM EXECUTION STARTS HERE
    
FF=0
while(FF!=1 and FF!=2 and FF!=3):                           #CHOOSING THE FLIP FLOP
        print("CHOOSE THE FLIP FLOP TO BE USED:\n\
1. JK FLIP FLOP\n\
2. D FLIP FLOP\n\
3. T FLIP FLOP")
        FF=eval(input("(ENTER EITHER 1 OR 2 OR 3):"))
        if(FF!=1 and FF!=2 and FF!=3):
                print("PLEASE ENTER A VALID INPUT")
                
print("\nTHE MAXIMUM ALLOWED STATE IS 15")
seq_int=list(eval(input("\nENTER THE SEQUENCE OF THE COUNTER:")))
n=len(seq_int)
m=len(str(bin(max(seq_int)).replace("0b","")))

print("\nNUMBER OF ELEMENTS IN THE SEQUENCE:",n)
print("\nNUMBER OF FLIPFLOPS REQUIRED:",m)                                        

q_t1=[]         #ASSIGNING THE PRESENT STATES
for i in range(0,n):
    a=str(bin(seq_int[i]).replace("0b",""))
    a=zeros(m-len(a))+a
    q_t1.append(a)
print("\nPRESENT STATES (Q(t)):",q_t1)
q1_str=""
for i in range(0,n):
    q1_str+=q_t1[i]

q_t2=[]         #ASSIGNING THE NEXT STATES
q_t2=q_t1[1:]+q_t1[0:1]
print("\nNEXT STATES (Q(t+1)):",q_t2)
q2_str=""
for i in range(0,n):
    q2_str+=q_t2[i]

if (m==1):      #GENERATING LIST OF ALL STATES
        all_states=[0,1]
elif (m==2):
        all_states=[0,1,2,3]
elif (m==3):
        all_states=[0,1,2,3,4,5,6,7]
elif (m==4):
        all_states=[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]
else:
        print("The number of states exceeds the limit")

if (FF==1):     #JK FLIP FLOP
        for i in range(m-1,-1,-1):
                j_k_ff(i)

elif (FF==2):   #D FLIP FLOP
        for i in range(m-1,-1,-1):
                d_ff(i)
else:           #T FLIP FLOP
        for i in range(m-1,-1,-1):
                t_ff(i)

#END
