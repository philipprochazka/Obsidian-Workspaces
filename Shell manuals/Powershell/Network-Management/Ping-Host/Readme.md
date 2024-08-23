NAME
    Ping-Host

SYNOPSIS
    PSCX Cmdlet: Sends ICMP echo requests to network hosts.


SYNTAX
    Ping-Host [-HostName] <PSObject[]> [[-Count] <Int32>] [-NoDnsResolution] [-Quiet] [[-BufferSize] <Int32>] [[-Timeou
    t] <Int32>] [[-TTL] <Int32>] [[-AllAddresses]] [[-Asynchronous]] [<CommonParameters>]


DESCRIPTION
    Sends ICMP echo requests to network hosts.


PARAMETERS
    -HostName <PSObject[]>


        Required?                    true
        Position?                    1
        Default value
        Accept pipeline input?       true (ByValue)
        Accept wildcard characters?  false

    -Count <Int32>
        Number of messages to send to each address.