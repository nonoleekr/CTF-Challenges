# Hex to ASCII Conversion Challenge

## Challenge Context
In this challenge, I encountered a network service running on `skrctf.me` at port `3012`. Instead of using their provided web shell, which I found inconvenient, I decided to interact with the service using my own PowerShell terminal script.

## Approach
I wrote a PowerShell TCP client script that connects to the target host and port, listens for a hex challenge from the server, and sends back the ASCII equivalent.

The server sends 4 bytes of hexadecimal data and expects the corresponding ASCII string in response. The challenge consists of 5 such questions, each requiring quick and correct answers within 60 seconds.

## PowerShell Script Used

```
# Connect to TCP server
$tcp = New-Object System.Net.Sockets.TcpClient('skrctf.me', 3012)
$stream = $tcp.GetStream()

# Function to send ASCII string as raw bytes (end with newline)
function Send-AsciiString([string]$str) {
    $bytes = [System.Text.Encoding]::ASCII.GetBytes($str + "`n")
    $stream.Write($bytes, 0, $bytes.Length)
}

# Function to read all available bytes and convert to ASCII string
function Read-Available() {
    $output = ""
    while ($tcp.Client.Available -gt 0) {
        $buffer = New-Object byte[] 1024
        $bytesRead = $stream.Read($buffer, 0, $buffer.Length)
        if ($bytesRead -gt 0) {
            $output += [System.Text.Encoding]::ASCII.GetString($buffer, 0, $bytesRead)
        }
        Start-Sleep -Milliseconds 50
    }
    return $output
}

# Read initial server prompt
Start-Sleep -Milliseconds 700
$response = Read-Available
Write-Output $response

# Interactive loop for 5 questions
for ($i = 1; $i -le 5; $i++) {
    # Extract hex string from response (e.g. "Hex: 72756666")
    if ($response -match "Hex:\s*([0-9a-fA-F]{8})") {
        $hexString = $matches[9]
        
        # Convert hex string to ASCII text
        $ascii = -join ((0..($hexString.Length-1) | Where-Object { $_ % 2 -eq 0 }) | ForEach-Object {
            [char][convert]::ToByte($hexString.Substring($_, 2), 16)
        })

        # Send ASCII answer
        Send-AsciiString $ascii
    } else {
        # If no hex found, send blank line
        Send-AsciiString ""
    }

    # Wait and read next prompt / result
    Start-Sleep -Milliseconds 700
    $response = Read-Available
    Write-Output $response
}

# Close connection
$tcp.Close()
```

## Result
Running this script against the server automatically solves the challenge question by converting hex to ASCII and submitting the correct answers. The flag was revealed without any manual input:

```
SKR{S1mpl3_H3x_t0_45cII}
```

## Conclusion
Using a custom scripted terminal client allowed me to automate interaction with the challenge service, bypassing the clunky web shell interface and efficiently solving the hex-to-ASCII challenge under time constraints. This approach highlights the power of scripting in solving CTF challenges quickly and reliably.
