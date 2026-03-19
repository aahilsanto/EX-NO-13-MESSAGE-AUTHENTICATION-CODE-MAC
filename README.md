# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:

```python
MAC_SIZE = 32

def compute_mac(key, message):
    mac = []
    key_len = len(key)
    msg_len = len(message)

    for i in range(MAC_SIZE):
        xor_byte = ord(key[i % key_len]) ^ ord(message[i % msg_len])
        mac.append(xor_byte)
    return mac  

def mac_to_hex(mac):
    return ''.join(format(b, '02x') for b in mac)

def hex_to_mac(hex_string):
    mac = []
    for i in range(0, MAC_SIZE * 2, 2):
        mac.append(int(hex_string[i:i+2], 16))
    return mac

key = input("Enter the secret key: ")
message = input("Enter the message: ")
mac = compute_mac(key, message)
print("Computed MAC (in hex):")
print(" ", mac_to_hex(mac))
received_mac_hex = input("Enter the received MAC (as hex): ")
received_mac = hex_to_mac(received_mac_hex)

if mac == received_mac:
    print("MAC verification successful. Message is authentic.")
else:
    print("MAC verification failed. Message is not authentic.")
```

## Output:

<img width="807" height="272" alt="image" src="https://github.com/user-attachments/assets/becabb9a-1134-4c49-bea5-185933c89c27" />

## Result:
The program is executed successfully.
