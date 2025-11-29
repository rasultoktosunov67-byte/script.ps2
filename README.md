# script.ps2
dd-Type -AssemblyName System.Windows.Forms
Start-Sleep -Milliseconds 200
[System.Windows.Forms.SendKeys]::SendWait("{F11}")
Start-Sleep -Milliseconds 300-

$skull = @'
          .                                                      .
        .n                   .                 .                  n.
  .   .dP                  dP                   9b                 9b.    .
 4    qXb         .       dX                     Xb       .        dXp     t
dX.    9Xb      .dXb    __                         __    dXb.     dXP     .Xd
9XXb._       _.dXXXXb dXXXXbo.                 .odXXXXb dXXXXb._       _.dXXP
 9XXXXXXXXXXXXXXXXXXXVXXXXXXXXOo.           .oOXXXXXXXXVXXXXXXXXXXXXXXXXXXXP
  `9XXXXXXXXXXXXXXXXXXXXX'~   ~`OOO8b   d8OOO'~   ~`XXXXXXXXXXXXXXXXXXXXXP'
    `9XXXXXXXXXXXP' `9XX'          `98v8P'           `XXP' `9XXXXXXXXXXXP'
        ~~~~~~~~      9X.          .db|db.          .XP      ~~~~~~~~
                      )b.  .dbo.dP'`v'`v'`9b.odb.  .d( 
                    ,dXXXXXXXXXXXb     ) (     dXXXXXXXXXXXb.
                   dXXXXXXXXXXXP'      `v'      `9XXXXXXXXXXXb
                  dXXXXXXXXXXXP                    9XXXXXXXXXXXb
                 dXXXXXXXXXXXXb                    dXXXXXXXXXXXXb
                 9XXb'   `XXXXXb                  dXXXXX'   `dXXP
                  `'       `XXXXb                dXXXX'       `'
                            `XXXXXb            dXXXXX'
                              `XXXXXb        dXXXXX'
                                `XXXXb.    .dXXXX'
                                  `XXXXXXXXXXX'
                                    `XXXXXXX'
'@

$chars = "@#%&$+=-<>/\|█▓▒░"
$maxWidth = 120

function Glitch-Line {
    param($length)
    $line = ""
    for ($i=0; $i -lt $length; $i++) {
        $line += $chars[(Get-Random -Minimum 0 -Maximum $chars.Length)]
    }
    return $line
}

function Glitch-Skull {
    param($skull)
    $lines = $skull -split "`n"
    foreach ($line in $lines) {
        $roll = Get-Random -Minimum 1 -Maximum 6
        switch ($roll) {
            1 { Write-Host (Glitch-Line $line.Length) -ForegroundColor White }
            2 { 
                $half = $line.Substring(0, [Math]::Floor($line.Length/2))
                Write-Host (($half) + (Glitch-Line ($line.Length - $half.Length))) -ForegroundColor DarkRed
            }
            3 { 
                $shift = " " * (Get-Random -Minimum 0 -Maximum 10)
                Write-Host ($shift + $line) -ForegroundColor DarkRed
            }
            default { Write-Host $line -ForegroundColor DarkRed }
        }
        Start-Sleep -Milliseconds 12
    }
}

function Aggressive-Phrases {
    $phrases = @(
        "OVERLOAD SEQUENCE",
        "STRUCTURE COLLAPSE",
        "CHANNEL SATURATION",
        "UNSTABLE FEEDBACK",
        "PEAK OUTPUT BREACH",
        "DATA NOISE RISING",
        "PRESSURE MAXIMUM",
        "SIGNAL FRACTURE"
    )
    for ($i=0; $i -lt 6; $i++) {
        Write-Host ("[!] " + $phrases[(Get-Random 0 $phrases.Count)]) -ForegroundColor White
        Write-Host (Glitch-Line (Get-Random -Minimum 60 -Maximum $maxWidth)) -ForegroundColor Red
        Start-Sleep -Milliseconds 45
    }
}

function Glitch-Block {
    param($lines)
    for ($i=0; $i -lt $lines; $i++) {
        Write-Host (Glitch-Line (Get-Random -Minimum 40 -Maximum $maxWidth)) -ForegroundColor Red
        Start-Sleep -Milliseconds 25
    }
}

Clear-Host
Write-Host "INITIALIZING TOTAL GLITCH CHAOS..." -ForegroundColor Red
Start-Sleep -Milliseconds 300
Clear-Host

while ($true) {

    Glitch-Block -lines 10

    Clear-Host
    Glitch-Skull $skull

    Aggressive-Phrases

    for ($i=0; $i -lt 30; $i++) {
        Write-Host (Glitch-Line (Get-Random -Minimum 20 -Maximum $maxWidth)) -ForegroundColor DarkRed
    }

    Start-Sleep -Milliseconds 120
    Clear-Host
}
