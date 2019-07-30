# Code commenting practices

**1.**    **Comments are not subtitles**

BAD:

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><code>// Loop through all bananas in the bunch</code>
        </p>
        <p><code>foreach(banana b in</code>  <code>bunch) {</code>
        </p>
        <p><code>    monkey.eat(b);  //make the monkey eat one banana</code>
        </p>
        <p><code>}</code>
        </p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>**Exceptions:**

* Code examples used to teach a concept or new programming language.
* Programming languages that aren’t remotely human readable \(Assembly, Perl\)

**2.**    **Comments are not an art project** \(don’t try to pay attention to your code with drawing monkeys, smiles etc.\)

**3.**    **Header Blocks: Nuisance or Menace?**

1\) Blocks of header comments at the top of every file, method or class are enablers for badly named objects/methods – Of course, header blocks aren’t the cause for badly named identifiers, but they are an easy excuse to not  put in the work to come up with meaningful names, an often deceptively difficult task.

2\) They never get updated: We all know that methods are supposed to remain short and sweet, but real life gets in the way and before you know it you have a 4K line class and the header block is scrolled off of the screen in the IDE 83% of the time

**Exception:** Some languages \(Java/C\#\) have tools that can digest specially formatted header block comments into documentation or Intellisense/Autocomplete hints. Still, remember rule \(2\) and stick to the minimum required by the tool and draw the line at creating any form of ASCII art.

**4.**    **Comments are not source control**

**BAD 1: “The Historian”**

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>1</p>
        <p>2</p>
        <p>3</p>
        <p>4</p>
        <p>5</p>
        <p>6</p>
        <p>7</p>
        <p>8</p>
        <p>9</p>
      </th>
      <th style="text-align:left">
        <p><code>// method name: pityTheFoo (included for the sake of redundancy)</code>
        </p>
        <p><code>// created: Feb 18, 2009 11:33PM</code>
        </p>
        <p><code>// Author: Bob</code>
        </p>
        <p><code>// Revisions: Sue (2/19/2009) - Lengthened monkey&apos;s arms</code>
        </p>
        <p><code>//            Bob (2/20/2009) - Solved drooling issue</code>
        </p>
        <p><code>void</code>  <code>pityTheFoo() {</code>
        </p>
        <p><code>     ...</code>
        </p>
        <p><code>}</code>
        </p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>**BAD 2: “The Code Hoarder”**

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>1</p>
        <p>2</p>
        <p>3</p>
        <p>4</p>
        <p>5</p>
        <p>6</p>
        <p>7</p>
        <p>8</p>
      </th>
      <th style="text-align:left">
        <p><code>void</code>  <code>monkeyShines() {</code>
        </p>
        <p><code>     if</code>  <code>(monkeysOnBed(Jumping).count &gt; max) {</code>
        </p>
        <p><code>        monkeysOnBed.breakHead();</code>
        </p>
        <p><code>        // code removed, smoothie shop closed.</code>
        </p>
        <p><code>        // leaving it in case a new one opens.</code>
        </p>
        <p><code>        // monkeysOnBed.Drink(BananaSmoothie);</code>
        </p>
        <p><code>     }</code>
        </p>
        <p><code>}</code>
        </p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>**5.**     **Comments are a code smell**

Whenever you think, “This code needs a comment” follow that thought with, “How could I modify the code so its purpose is obvious?”  
Talk with your code, not your comments.

