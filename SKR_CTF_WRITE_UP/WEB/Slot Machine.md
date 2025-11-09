# Slot Machine Challenge Write-up

## Hints

> **Hint 1:** Is there any way to decrease the bet?  
> **Hint 2:** Can bet be negative?

---

## Initial Exploration

Start by interacting with the slot machine game:

* Press **Spin**
* Try **increasing** and **decreasing** the bet

After experimenting, you’ll notice something interesting —
the **bet value can go negative**.

---

## Inspecting the Source

Open the browser’s **Developer Tools** → **Sources** tab.
Inspect the JavaScript file named **`slotEngine.js`**.

Inside, you’ll find the logic that updates your balance when you lose:

```javascript
price = price - bet;
```

If the bet is **negative**, this becomes:

```javascript
price = price - (-bet);
```

Which simplifies to:

```javascript
price = price + bet;
```

So instead of losing money, you actually **gain** money.

---

## Exploit: Editing the Script

To speed things up (instead of clicking decrease a billion times),
modify the **down** function that decreases your bet.

Original code:

```javascript
$("#down").click(function() {
    var bet = +($("#bets").text()) - 1;
    $("#bets").text(bet);
});
```

Change it to:

```javascript
$("#down").click(function() {
    var bet = +($("#bets").text()) - 1000000000;
    $("#bets").text(bet);
});
```

---

## Overriding the Script

1. **Right-click** the page and select **Override Content**.
2. **Save** your modified `slotEngine.js` in the override folder.
3. Refresh the page if needed.

Now, click the **Down** button — your bet will instantly become **-1,000,000,000**.

---

## Triggering the Win

Simply **spin and lose** with a negative bet.

Because of the logic we found earlier, your credits will increase to over a **billion**.
A popup will appear with the flag.

---

## Flag

```
SKR{1_become_4_Bi110naire_s0_fr3ak1ng_F45T_460c10}
```
