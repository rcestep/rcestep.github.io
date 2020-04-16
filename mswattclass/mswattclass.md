## Ms. Watt's Class
-------------------------

Ms. Watt's class for Python really challenged me hard because this was an instructor who knew what to look for in code and made sure that her students became meticulous in all their work by really challenging us to get the code and make sure there was no room for mistakes!!  That class although rough gave me the skill to really be thorough with my work and make sure that I fixed anything and everything I could.  With that class, the final project that I had done was make a Python script that made a subnet table for departments and made the subnet table out using Python and using the inputs from the user.  The code is below!
```Python
# Programmer:   Roland Estep
# Date:         3 December 2019
# Chapter:      not from book
# Exercise:     Final Project
# Purpose:      Subnet IP addresses and calculate the total hosts, the average
#               number of hosts, and display the subnet chart

def main():

    # variables being used
    nameDepartment = ''     # string
    numDepartments = 0      # int
    firstNAOctet = 0        # int
    secondNAOctet = 0       # int
    thirdNAOctet = 0        # int
    fourthNAOctet = 0       # int
    networkAddress = ''     # string
    firstFAOctet = 0        # int
    secondFAOctet = 0       # int
    thirdFAOctet = 0        # int
    fourthFAOctet = 0       # int
    firstAvailAddress = ''  # string
    firstLAOctet = 0        # int
    secondLAOctet = 0       # int
    thirdLAOctet = 0        # int
    fourthLAOctet = 0       # int
    lastAvailAddress = ''   # int
    firstBAOctet = 0        # int
    secondBAOctet = 0       # int
    thirdBAOctet = 0        # int
    fourthBAOctet = 0       # int
    broadcastAddress = ''   # string
    numNetBits = 0          # int
    numHostBits = 0         # int
    numHosts = 0            # int
    totalHosts = 0          # int
    averageHosts = 0        # int
    firstSMOctet = 0        # int
    secondSMOctet = 0       # int
    thirdSMOctet = 0        # int
    fourthSMOctet = 0       # int
    subnetMask = ''         # string
    increment = 0           # int

    # write the heading of the chart
    outputFile = writeChartHeading()

    # get the name of the department
    nameDepartment = getNameDepartment()

    # start the while loop
    while nameDepartment != '':

        # get the first octet of the network address
        firstNAOctet = getFirstOctet()

        # get the sedond octet of the network address
        secondNAOctet = getSecondOctet(firstNAOctet)

        # get the third octet of the network address
        thirdNAOctet = getThirdOctet()

        # get the fourth octet of the network address
        fourthNAOctet = getFourthOctet()

        # get the network address
        networkAddress = str(firstNAOctet) + '.' + str(secondNAOctet) + '.' + str(thirdNAOctet) + '.' + str(fourthNAOctet)

        # get the number of network bits being used
        numNetBits = getNumberNetBits()

        # calculate the increment being used
        increment = determineIncrement(numNetBits)

        # calculate the subnet mask
        subnetMask = calcSubnetMask(numNetBits)

        # calculate the number of hosts for the subnet
        numHosts = calcNumHosts(numNetBits)

        # keep a running total of total hosts
        totalHosts += numHosts

        # keep a running total of number of departments
        numDepartments += 1

        # calculate the average number of hosts per subnet
        averageHosts = calcAverageHosts(totalHosts,numDepartments)# calculate the first available address of the subnetwork
        firstAvailAddress = calcFAAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet)

        # calculate the last available address of the subnetwork
        lastAvailAddress = calcLAAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet,increment,numNetBits)

        # calculate the broadcast of the subnetwork
        broadcastAddress = calcBCAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet,increment,numNetBits)

        # append the network to the output file
        writeNetwork(nameDepartment,networkAddress,firstAvailAddress,lastAvailAddress,broadcastAddress,subnetMask,numHosts,outputFile)

        # get the next name of the department
        nameDepartment = getNameDepartment()

    # append the total hosts, average hosts, and the number of departments
    # as well as the author statement
    writeEndingLines(totalHosts,averageHosts,numDepartments,outputFile)
    

################################################################################
# This function will ask for the name of the department
def getNameDepartment():
    # variables being used
    nameDepartment = ''     # string

    # get the name of the department
    nameDepartment = str(input('Enter the department you plan to subnet (or press Enter to quit):  '))
    return nameDepartment

################################################################################
# This function will get the first octet of the network address to be subnetted
def getFirstOctet():
    # variables being used
    firstNAOctet = 0        # int

    # get the first octet
    firstNAOctet = int(input('Enter the first octet of the network address to be subnetted:  '))

    # validate the first octet
    while firstNAOctet != 10 and firstNAOctet != 172 and firstNAOctet != 192:
        print('Invalid octet input.  Input must be either 10, 172, or 192.')
        firstNAOctet = int(input('Enter the first octet of the network address to be subnetted:  '))
    return firstNAOctet

################################################################################
# This function will get the second octet of the network address to be subnetted
def getSecondOctet(firstNAOctet):
    # variables being used
    secondNAOctet = 0       # int

    # get the second octet
    secondNAOctet = int(input('Enter the second octet of the network address to be subnetted:  '))

    # validate the second octet
    if firstNAOctet == 10:
        while secondNAOctet < 0 or secondNAOctet > 255:
            print('Invalid octet input.  Input must be between 0 and 255.')
            secondNAOctet = int(input('Enter the second octet of the network address to be subnetted:  '))
    elif firstNAOctet == 172:
        while secondNAOctet < 16 or secondNAOctet > 31:
            print('Invalid octet input.  Input must be between 16 and 31.')
            secondNAOctet = int(input('Enter the second octet of the network address to be subnetted:  '))
    else:
        while secondNAOctet != 168:
            print('Invalid octet input.  Input must be 168.')
            secondNAOctet = int(input('Enter the second octet of the network address to be subnetted:  '))
    return secondNAOctet

################################################################################
# This function will get the third octet of the network address to be subnetted
def getThirdOctet():
    # variables being used
    thirdNAOctet = 0        # int

    # get the third octet
    thirdNAOctet = int(input('Enter the third octet of the network address to be subnetted:  '))

    # validate the third octet
    while thirdNAOctet < 0 or thirdNAOctet > 255:
        print('Invalid octet input.  Input must be between 0 and 255.')
        thirdNAOctet = int(input('Enter the third octet of the network address to be subnetted:  '))
    return thirdNAOctet

################################################################################
# This function will get the fourth octet of the network address to be subnetted
def getFourthOctet():
    # variables being used
    fourthNAOctet = 0       # int

    # get the fourth octet
    fourthNAOctet = int(input('Enter the fourth octet of the network address to be subnetted:  '))

    # validate the fourth octet
    while fourthNAOctet < 0 or fourthNAOctet > 255:
        print('Invalid octet input.  Input must be between 0 and 255.')
        fourthNAOctet = int(input('Enter the fourth octet of the network address to be subnetted:  '))
    return fourthNAOctet

################################################################################
# This function will get the number of bits being used in the subnet mask
def getNumberNetBits():
    # variables being used
    numNetBits = 0      # int

    # get the number of network bits to be used
    numNetBits = int(input('Enter the amount of network bits that will be used in the subnet mask:  '))

    # validate the number
    while numNetBits < 8 or numNetBits > 31:
        print('Invalid number of bits.  Must be between 8 and 31.')
        numNetBits = int(input('Enter the amount of bits that will be used in the subnet mask:  '))
    return numNetBits

################################################################################
# This function will calculate the network increment
def determineIncrement(numNetBits):
    # variables being used
    increment = 0       # int

    # determine the increment
    if numNetBits == 9 or numNetBits == 17 or numNetBits == 25:
        increment = 128
    elif numNetBits == 10 or numNetBits == 18 or numNetBits == 26:
        increment = 64
    elif numNetBits == 11 or numNetBits == 19 or numNetBits == 27:
        increment = 32
    elif numNetBits == 12 or numNetBits == 20 or numNetBits == 28:
        increment = 16
    elif numNetBits == 13 or numNetBits == 21 or numNetBits == 29:
        increment = 8
    elif numNetBits == 14 or numNetBits == 22 or numNetBits == 30:
        increment = 4
    elif numNetBits == 15 or numNetBits == 23 or numNetBits == 31:
        increment = 2
    else:
        increment = 1
    return increment

################################################################################
# This function will calculate the first available address for the network
def calcFAAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet):
    # variables being used
    firstFAOctet = 0        # int
    secondFAOctet = 0       # int
    thirdFAOctet = 0        # int
    fourthFAOctet = 0       # int

    # calculate the first available address
    firstFAOctet = firstNAOctet
    secondFAOctet = secondNAOctet
    thirdFAOctet = thirdNAOctet
    fourthFAOctet = fourthNAOctet + 1

    # concatenate into a string
    firstAvailAddress = str(firstFAOctet) + '.' + str(secondFAOctet) + '.' + str(thirdFAOctet) + '.' + str(fourthFAOctet)
    return firstAvailAddress

################################################################################
# This function will calculate the last available address for the network
def calcLAAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet,increment,numNetBits):

    # variables being used
    firstLAOctet = 0        # int
    secondLAOctet = 0       # int
    thirdLAOctet = 0        # int
    fourthLAOctet = 0       # int

    # calculate the last available address
    firstLAOctet = firstNAOctet
    if numNetBits == 8:
        secondLAOctet = 255
        thirdLAOctet = 255
        fourthLAOctet = 254
    elif numNetBits > 8 and numNetBits <= 15:
        secondLAOctet = increment - 1
        thirdLAOctet = 255
        fourthLAOctet = 254
    elif numNetBits == 16:
        secondLAOctet = secondNAOctet
        thirdLAOctet = 255
        fourthLAOctet = 254
    elif numNetBits > 16 and numNetBits <= 23:
        secondLAOctet = secondNAOctet
        thirdLAOctet = increment - 1
        fourthLAOctet = 254
    elif numNetBits == 24:
        secondLAOctet = secondNAOctet
        thirdLAOctet = thirdNAOctet
        fourthLAOctet = 254
    else:
        secondLAOctet = secondNAOctet
        thirdLAOctet = thirdNAOctet
        fourthLAOctet = increment - 2

    # concatenate into a string
    lastAvailAddress = str(firstLAOctet) + '.' + str(secondLAOctet) + '.' + str(thirdLAOctet) + '.' + str(fourthLAOctet)
    return lastAvailAddress

################################################################################
# This function will calculate the broadcast address for the network
def calcBCAddress(firstNAOctet,secondNAOctet,thirdNAOctet,fourthNAOctet,increment,numNetBits):
    # variables being used
    firstBAOctet = 0        # int
    secondBAOctet = 0       # int
    thirdBAOctet = 0        # int
    fourthBAOctet = 0       # int

    # calculate the broadcast address
    firstBAOctet = firstNAOctet
    if numNetBits == 8:
        secondBAOctet = 255
        thirdBAOctet = 255
        fourthBAOctet = 255
    elif numNetBits > 8 and numNetBits <= 15:
        secondBAOctet = increment - 1
        thirdBAOctet = 255
        fourthBAOctet = 255
    elif numNetBits == 16:
        secondBAOctet = secondNAOctet
        thirdBAOctet = 255
        fourthBAOctet = 255
    elif numNetBits > 16 and numNetBits <= 23:
        secondBAOctet = secondNAOctet
        thirdBAOctet = increment - 1
        fourthBAOctet = 255
    elif numNetBits == 24:
        secondBAOctet = secondNAOctet
        thirdBAOctet = thirdNAOctet
        fourthBAOctet = 255
    else:
        secondBAOctet = secondNAOctet
        thirdBAOctet = thirdNAOctet
        fourthBAOctet = increment - 1

    # concatenate int a string
    broadcastAddress = str(firstBAOctet) + '.' + str(secondBAOctet) + '.' + str(thirdBAOctet) + '.' + str(fourthBAOctet)
    return broadcastAddress

################################################################################
# This function calculates how many host addresses are available in each subnet
def calcNumHosts(numNetBits):
    # variables being used
    numHostBits = 0         # int
    numHosts = 0            # int

    # calculate the number of hosts
    numHostBits = 32 - numNetBits
    numHosts = (2**numHostBits) - 2
    return numHosts

################################################################################
# This function will calculate the average number of hosts per network
def calcAverageHosts(totalHosts,numDepartments):
    # variables being used
    averageHosts = 0        # int

    # calculate the average number of hosts
    averageHosts = totalHosts // numDepartments
    return averageHosts

################################################################################
# This function will determine the subnet mask of the network
def calcSubnetMask(numNetBits):
    # variables being used
    firstSMOctet = 0        # int
    secondSMOctet = 0       # int
    thirdSMOctet = 0        # int
    fourthSMOctet = 0       # int

    # calculate the subnet mask
    if numNetBits >= 24:
        firstSMOctet = 255
        numNetBits = numNetBits - 8
        secondSMOctet = 255
        numNetBits = numNetBits - 8
        thirdSMOctet = 255
        numNetBits = numNetBits - 8
        if numNetBits == 0:
            fourthSMOctet = 0
        elif numNetBits == 1:
            fourthSMOctet = 128
        elif numNetBits == 2:
            fourthSMOctet = 192
        elif numNetBits == 3:
            fourthSMOctet = 224
        elif numNetBits == 4:
            fourthSMOctet = 240
        elif numNetBits == 5:
            fourthSMOctet = 248
        elif numNetBits == 6:
            fourthSMOctet = 252
        else:
            fourthSMOctet = 254
    elif numNetBits >= 16:
        firstSMOctet = 255
        numNetBits = numNetBits - 8
        secondSMOctet = 255
        numNetBits = numNetBits - 8
        if numNetBits == 0:
            thirdSMOctet = 0
        elif numNetBits == 1:
            thirdSMOctet = 128
        elif numNetBits == 2:
            thirdSMOctet = 192
        elif numNetBits == 3:
            thirdSMOctet = 224
        elif numNetBits == 4:
            thirdSMOctet = 240
        elif numNetBits == 5:
            thirdSMOctet = 248
        elif numNetBits == 6:
            thirdSMOctet = 252
        else:
            thirdSMOctet = 254
        fourthSMOctet = 0
    else:
        firstSMOctet = 255
        numNetBits = numNetBits - 8
        if numNetBits == 0:
            secondSMOctet = 0
        elif numNetBits == 1:
            secondSMOctet = 128
        elif numNetBits == 2:
            secondSMOctet = 192
        elif numNetBits == 3:
            secondSMOctet = 224
        elif numNetBits == 4:
            secondSMOctet = 240
        elif numNetBits == 5:
            secondSMOctet = 248
        elif numNetBits == 6:
            secondSMOctet = 252
        else:
            secondSMOctet = 254
        thirdSMOctet = 0
        fourthSMOctet = 0

    # concatenate into a string
    subnetMask = str(firstSMOctet) + '.' + str(secondSMOctet) + '.' + str(thirdSMOctet) + '.' + str(fourthSMOctet)
    return subnetMask

################################################################################
# This function writes the chart heading
def writeChartHeading():

    # open the output file for writing
    outputFile = open('subnetting.txt','w')

    # write the heading
    outputFile.write('\t\t\t\t\t\t\tSubnets of Departments\n'
                     '\n' + 
                     '  ' + format('Name','10s') + '    ' + format('Net Address','15s') + '  ' + format('FA Address','15s') + '   ' + format('LA Address','15s') + '     ' + format('Broadcast','15s') + '     ' + format('SubnetMask','15s') + '   ' + format('Number of Hosts','20s') + '\n'
                     '-------------------------------------------------------------------------------------------------------------------------------\n')
    return outputFile

################################################################################
# This function appends the subnetted network
def writeNetwork(nameDepartment,networkAddress,firstAvailAddress,lastAvailAddress,broadcastAddress,subnetMask,numHosts,outputFile):

    # append the inputs and processes
    outputFile.write('  ' + format(nameDepartment,'10s') + '    ' + format(networkAddress,'15s') + '  ' + format(firstAvailAddress,'15s') + '   ' + format(lastAvailAddress,'15s') + '     ' + format(broadcastAddress,'15s') + '     ' + format(subnetMask,'15s') + '       ' + format(numHosts,',d') + '\n')

################################################################################
# This function appends the total hosts, average number of hosts, and author statement
def writeEndingLines(totalHosts,averageHosts,numDepartments,outputFile):
    
    # append the total hosts, average hosts, and author statement
    outputFile.write('\n\t\t\t\t\t\t\t\t\t\t          Total Number of Hosts: ' + format(totalHosts,',d') + '\n')
    outputFile.write('\t\t\t\t\t\t\t\t\t\t        Average Number of Hosts: ' + format(averageHosts,',d') + '\n')
    outputFile.write('There were ' + str(numDepartments) + ' department(s) subnetted.' + '\n')
    outputFile.write('This document was produced by Roland Estep.')

    # close the file
    outputFile.close()


main()
```

With Ms. Watt's teaching, I really got an understanding of how a programmers mind should operate and I grew a fondness for coding, so much that I decided to pursue more and more knowledge about coding and languages that I don't quite know yet!

Go back to [Home](https://rcestep.github.io)!

[Mr Cain's Classes](https://rcestep.github.io/mrcainclass/mrcainclass.html)

[Ms. Shoemaker's Classes](https://rcestep.github.io/msshoemakerclass/msshoemakerclass.html)

[Mr. Hicks' Classes](https://rcestep.github.io/mrhicksclass/mrhicksclass.html)

[Mr. Benfield's Class](https://rcestep.github.io/mrbenfieldclass/mrbenfieldclass.html)

[Mr. Theisen's Classes](https://rcestep.github.io/mrtheisenclass/mrtheisenclass.html)

[Mitchell Technological Society](https://rcestep.github.io/mts/mts.html)

[My Other Accomplishments](https://rcestep.github.io/other/other.html)

[LinkedIn](https://linkedin.com/in/roland-c-estep) | [GitHub](https://github.com/rcestep) | [Discord](https://discordhub.com/profile/532348150019522580)
-------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------
Email: **roland.estep@outlook.com**                | Phone: **(980)892-2512**             | [Reddit](https://reddit.com/user/rcmoonpie1)
