## Παράρτημα Α: Λέξεις-Κλειδιά

Η παρακάτω λίστα περιέχει λέξεις κλειδιά που έχουν δεσμευτεί για χρήση τώρα
ή στο μέλλον από την γλώσσα Rust. Οπότε, δεν μπορούν να χρησιμοποιηθούν ως
αναγνωριστικά (εκτός σαν |raw| αναγνωριστικά όπως θα συζητήσουμε στην ενότητα “[Raw
Identifiers][raw-identifiers]<!-- ignore -->” ). Αναγνωριστικά είναι τα ονόματα
συναρτήσεων, μεταβλητών, παραμέτρων, πεδίων δομών, |modules|, κιβώτια, σταθερές,
|macros|, στατικές τιμές, γνωρίσματα, τύποι, |traits|, ή |lifetimes|.

[raw-identifiers]: #raw-identifiers

### Λέξεις Κλειδιά που βρίσκονται τώρα σε χρήση

Η παρακάτω λίστα είναι μια λίστα λέξεων κλειδιών τώρα σε χρήση, με περιγραφή
της λειτουργικότητάς τους.

* `as` - perform primitive casting, disambiguate the specific trait containing
  an item, or rename items in `use` statements
* `async` -  return a `Future` instead of blocking the current thread
* `await` - suspend execution until the result of a `Future` is ready
* `break` - exit a loop immediately
* `const` - define constant items or constant raw pointers
* `continue` - continue to the next loop iteration
* `crate` - in a module path, refers to the crate root
* `dyn` - dynamic dispatch to a trait object
* `else` - fallback for `if` and `if let` control flow constructs
* `enum` - define an enumeration
* `extern` - link an external function or variable
* `false` - Boolean false literal
* `fn` - define a function or the function pointer type
* `for` - loop over items from an iterator, implement a trait, or specify a
  higher-ranked lifetime
* `if` - branch based on the result of a conditional expression
* `impl` - implement inherent or trait functionality
* `in` - part of `for` loop syntax
* `let` - bind a variable
* `loop` - loop unconditionally
* `match` - match a value to patterns
* `mod` - define a module
* `move` - make a closure take ownership of all its captures
* `mut` - denote mutability in references, raw pointers, or pattern bindings
* `pub` - denote public visibility in struct fields, `impl` blocks, or modules
* `ref` - bind by reference
* `return` - return from function
* `Self` - a type alias for the type we are defining or implementing
* `self` - method subject or current module
* `static` - global variable or lifetime lasting the entire program execution
* `struct` - define a structure
* `super` - parent module of the current module
* `trait` - define a trait
* `true` - Boolean true literal
* `type` - define a type alias or associated type
* `union` - define a [union][union]<!-- ignore -->; is only a keyword when used
  in a union declaration
* `unsafe` - denote unsafe code, functions, traits, or implementations
* `use` - bring symbols into scope
* `where` - denote clauses that constrain a type
* `while` - loop conditionally based on the result of an expression

[union]: ../reference/items/unions.html

### Λέξεις κλειδιά που έχουν δεσμευτεί για μελλοντική χρήση

Οι παρακάτω λέξεις κλειδιά δεν έχουν ακόμα κάποια λειτουργικότητα αλλά 
είναι δεσμευμένα από την Rust για πιθανή μελλοντική χρήση.

* `abstract`
* `become`
* `box`
* `do`
* `final`
* `macro`
* `override`
* `priv`
* `try`
* `typeof`
* `unsized`
* `virtual`
* `yield`

### |Raw| Αναγνωριστικά

*|Raw| Αναγνωριστικά* είναι η σύνταξη που σου επιτρέπει να χρησιμοποιήσεις λέξεις
κλειδιά κάπου που κανονικά δεν θα επιτρεπόταν. Χρησιμοποιείς το |raw| αναγνωριστικό
βάζοντας το πρόθεμα `r#` στην λέξη-κλειδί.

Για παράδειγμα, το `match` είναι μία λέξη-κλειδί. Αν προσπαθήσεις να μεταγλωττίσεις
την παρακάτω συνάρτηση που χρησιμοποιεί το `match` ως το όνομά της:

*Raw identifiers* are the syntax that lets you use keywords where they wouldn’t
normally be allowed. You use a raw identifier by prefixing a keyword with `r#`.

For example, `match` is a keyword. If you try to compile the following function
that uses `match` as its name:

<span class="filename">Όνομα Αρχείου: src/main.rs</span>

```rust,ignore,does_not_compile
fn match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}
```

Θα πάρεις αυτό το μήνυμα σφάλματος:

```text
error: expected identifier, found keyword `match`
 --> src/main.rs:4:4
  |
4 | fn match(needle: &str, haystack: &str) -> bool {
  |    ^^^^^ expected identifier, found keyword
```

Το μήνυμα σφάλματος σου δείχνει ότι δεν μπορείς να χρησιμοποιήσεις την
λέξη-κλειδί `match` σαν αναγνωριστικό συνάρτησης. Για να χρησιμοποιήσεις
το `match` σαν όνομα συνάρτησης, πρέπει να χρησιμοποιήσεις την σύνταξη
για το |raw| αναγνωριστικό, έτσι:


<span class="filename">Όνομα Αρχείου: src/main.rs</span>

```rust
fn r#match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}
```

Αυτός ο κώδικας θα μεταγλωττιστεί χωρίς μηνύματα σφάλματος. Σημείωσε ότι το 
`r#` πρόθεμα στο όνομα της συνάρτησης υπάρχει και στον ορισμό της και όταν
αυτή καλείται από την `main`.

|Raw| αναγνωριστικά επιτρέπουν την χρήση οποιασδήποτε λέξης επιλέξεις σαν
αναγνωριστικό, ακόμα και αν αυτό τυχαίνει να είναι μία δεσμευμένη λέξη κλειδί.
Αυτό μας δίνει περισσότερη ελευθερία να επιλέξουμε ονόματα αναγνωριστικών, και
μας επιτρέπει την ενσωμάτωση προγραμμάτων που έχουν γραφτεί σε κάποια γλώσσα
όπου αυτές οι λέξεις δεν είναι λέξεις κλειδιά. Επιπλέον, |raw| αναγνωριστικά
σου επιτρέπουν να χρησιμοποιήσεις βιβλιοθήκες γραμμένες σε κάποια διαφορετική
έκοδης Rust από αυτήν που χρησιμοποιεί το δικό σου κιβώτιο. Για παράδειγμα,
το `try` δεν είναι λέξη κλειδί στην έκδοση 2015 αλλά είναι στην έκδοση 2018.
Αν |depend| σε μία βιβλιοθήκη που έχει γραφτεί χρησιμοποιώντας την έκδοση 2015
και έχει μία συνάρτηση `try`, θα χρειαστεί να χρησιμοποιήσεις την σύνταξη |raw|
αναγνωριστικού, `r#try` σε αυτήν την περίπτωση, για να καλέσεις την συνάρτηση
από τον κώδικα σου που είναι στην έκδοση 2018. Βλέπε [Παράρτημα Ε][appendix-e]
<!-- ignore --> για περισσότερες πληροφορίες σχετικά με τις εκδόσεις.

[appendix-e]: appendix-05-editions.html
