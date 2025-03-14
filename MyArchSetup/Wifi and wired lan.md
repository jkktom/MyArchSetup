in arch linux
I want to test.
I just connected to this machine with both Lan and wifi. 
i want to know if both has strong connection to public network
how can I do that?

## Testing Network Connections

To test both your wired LAN and WiFi connections in Arch Linux, you can use several tools to check their strength, speed, and reliability:

### 1. Check Connection Status

First, verify both connections are active:

```bash
ip addr
```

Look for both interfaces (typically something like `wlan0` for WiFi and `eth0` or `enp3s0` for wired LAN) and confirm they have IP addresses.

### 2. Check Network Speed

#### Using speedtest-cli

Install it if you don't have it:

```bash
sudo pacman -S speedtest-cli
```

Test each connection separately:

```bash
# Disable WiFi temporarily to test wired connection
nmcli radio wifi off
speedtest-cli --simple
# Re-enable WiFi and disable wired to test WiFi
nmcli radio wifi on
# Disconnect wired (replace enp3s0 with your interface name)
sudo ip link set enp3s0 down
speedtest-cli --simple
# Re-enable wired
sudo ip link set enp3s0 up
```

#### Using iperf3

For more detailed testing, especially on your local network:

```bash
sudo pacman -S iperf
```

You'll need another computer on your network running iperf in server mode.

### 3. Check Connection Quality

Test latency and packet loss:

```bash
# Test ping to a reliable server (Google DNS)
ping -c 20 8.8.8.8
```

### 4. Check Signal Strength (WiFi only)

```bash
iwconfig
```

Look for "Signal level" in the output. Higher values (less negative) indicate stronger signals.

### 5. Monitor Network Traffic

Install and use tools like `nethogs` or `iftop`:

```bash
sudo pacman -S nethogs iftop
sudo nethogs
# or
sudo iftop
```

These tools will show you real-time network usage per interface.