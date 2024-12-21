# VaultDoor3

In this challenge there was a file `VaultDoor3.java` which was a java file.

```
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18gb41_u_4_mfr340");
    }
}
```

After seeing the code, I saw the last line which contained `jU5t_a_sna_3lpm18gb41_u_4_mfr340` and I wrapped this in the flag format thinking this could be the flag, but obviously I was wrong.
Running the program with the same flag also didn't give much insight, except a `Access denied!` message.

The hint was
`Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.`

So I started to analyze what the for loop code was doing and started creating a table.

First I wrote all the letters in `jU5t_a_sna_3lpm18gb41_u_4_mfr340` indiviually and numbered them.

![image](https://github.com/user-attachments/assets/2ed57059-a1e9-4ada-b5ec-5f3f733a464f)

In the first for loop, the first 8 charcaters are copied as it is into the buffer hwere the original password is being created.

![image](https://github.com/user-attachments/assets/fe577927-c496-4b69-9ad6-16f79da90335)

In the second for loop, the index 8 to 15 are reversed and addded to the buffer.

![image](https://github.com/user-attachments/assets/5748090a-6005-44d4-a900-92100fd021fb)

The third for loop, increments by +2 meaning the even indices are filled with the corresponding even indices from the last of the table.

The fourth for loop ensures that the odd indices are just filled with the corresponding values.

![image](https://github.com/user-attachments/assets/f096d6d2-7ad4-4dbc-b6ab-973437f4513c)


The final table is:

![image](https://github.com/user-attachments/assets/d3fd29bf-e5db-4ffb-808d-1d182f6c8869)

Deducing the flag from this, I got:

`FLAG: picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}`
