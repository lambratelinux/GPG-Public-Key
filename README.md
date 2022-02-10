# GPG-Public-Key
Generare la chiave pubblica e privata di Lambrate Linux 
Crearla con il programma font-end Seahorse (se non è installato: dnf install seahorse)
1) Pigiare su +
2) Chiave PGP
3) Inserire tutti i dati
4) pigiare Crea

$gpg --fingerprint 1BA95B50BC6DB5AE
pub   rsa4096 2022-02-07 [SC]
      D7D3 BBB8 B5B8 DC94 4744  6E56 1BA9 5B50 BC6D B5AE
uid           [ultimo] Lambrate Linux (Chiave usata per il sito lambratelinux.org) <info@lambratelinux.org>
sub   rsa4096 2022-02-07 [E]

FATTO!

# Esportare la chiave pubblica (per renderla leggibile in ASCII)

Digitare nel terminale il seguente comando :

  $gpg --export -a 1BA95B50BC6DB5AE > lambrate-linux-public.key

nel file "lambrate-linux-public.key " c'è la chiave pubblica generata ed esportare in formato ASCII (fatta con l'opzione -a del comando).

Questo file si potrebbe dare a tutti, ma prima bisogna firmarlo per garantirne l'autenticità e poi rigenerarlo con estensione .asc per dire a tutti che è in formato ASCII, solo a questo punro si può dare a tutti.
N.B.: Da questo punto in poi fare riferimento alla <dir> /home/idraulico/LambrateLinux-2021-Sito-WP/GPG-Key

# Firmare la chiave pubblica

Usare questo comando:
$gpg --local-user 1BA95B50BC6DB5AE --output lambrate-linux-public-key.sig --sign lambrate-linux-public.key
dove si riconosce:
1) l'UID           			--local-user 1BA95B50BC6DB5A
2) il file di output firmato	--output lambrate-linux-public-key.sig
3) il file da firmare (input)	--sign lambrate-linux-public.key

Il comando genera quindi un file con estensione .sig (che è la chiave pubblica firmata), in questo caso lambrate-linux-public-key.sig 

Nota bene: per firmare si può usare anche il comando interattivo:
$ gpg --edit-key UID     (gpg> help per aiuto, gpg> quit per uscire)
e successivamente il comando: sign 

# Verificare che la chiave pubblica sia firmata
Usare questo comando:
$ gpg --local-user D7D3BBB8B5B8DC9447446E561BA95B50BC6DB5AE --verify lambrate-linux-public-key.sig
gpg: Firma effettuata mer 9 feb 2022, 11:46:06 CET
gpg:                utilizzando la chiave RSA D7D3BBB8B5B8DC9447446E561BA95B50BC6DB5AE
gpg: Firma valida da "Lambrate Linux (Chiave usata per il sito lambratelinux.org) <info@lambratelinux.org>" [definitivo]

# Controllare che la chiave pubblica sia quella giusta (ovvero ricrearla con la firma)
Usare questo comando:
$ gpg --local-user 1BA95B50BC6DB5AE --output lambrate-linux-public-key.asc --decrypt lambrate-linux-public-key.sig
gpg: Firma effettuata mer 9 feb 2022, 11:46:06 CET
gpg:                utilizzando la chiave RSA D7D3BBB8B5B8DC9447446E561BA95B50BC6DB5AE
gpg: Firma valida da "Lambrate Linux (Chiave usata per il sito lambratelinux.org) <info@lambratelinux.org>" [definitivo]

[da qui in poi si è seguito quanto detto qui: https://www.gnupg.org/gph/en/manual/x135.html Paragrafo: Clearsigned documents]

Un uso comune delle firme digitali è quello di firmare post o messaggi di posta elettronica su usenet. In tali situazioni non è consigliabile comprimere il documento durante la firma. L'opzione --clearsign fa in modo che il documento venga racchiuso in una firma con armatura ASCII, ma in caso contrario non modifica il documento. 

Per fare questo dare il comando: 
gpg --local-user 1BA95B50BC6DB5AE --clearsign lambrate-linux-public-key.asc

che crea il file: lambrate-linux-public-key.asc.asc
Rinominarlo in: lambrate-linux-public-key-firmata.asc    che si può dare a tutti !

• -----BEGIN PGP SIGNED MESSAGE-----
• Hash: SHA256
•
• ------BEGIN PGP PUBLIC KEY BLOCK-----
• 
• mQINBGIBFggBEADtHOwg9JzBgpggska4B37l4l1HaTecBUF/wDR0y53Xcivl5hVu
• N5bdiYHOUHiy3JQBSd7iapH31U5lXZJk+G0fUfy84hpQO52Ha9Fl5cL9WA+I79Lf
• heWNUlT1GTQk9ATXNrz43AvFuVkTJWnWK/T5gZ9Lz73W+MXx+DTdTaFv9zgJOsSJ
• AanM8ZDS2JXAtICjbZT1Qi9e7ewy1hRCQJzEUOPqDy9mDu41CZWc+aASnYKPus6s
• bYlpQkp9ZR/XXoXFW8HVeCUA+XlMohv/o6MWKehXlItwYwmckJ0w5Z3gRcNTMFCV
• v8YBfGO076SVVEi7TpNsqG4LhLFPo2tLM2ZhGSlsJsqr80bjcIt4n90tUexhXOr1
• PVkpyLRO3s2CmEITcDKSn3H7Pt4f21Ue3L8rPAY0+57+Y9wuOoV0Rpse1oA0uSkh
• utYtlHLHbmVgLqMEIyus1e0aPZYFiMII2bZtMHAf0ejwxQ5mCbtwWaYmbyc6YLFr
• Qttcijrg7nc0LA/lw4SdFJ0iAtE5Gk7ps15qrczBU8ulVDGNU0LZxShLoz2AFxcq
• V8oMm+3DNCH0jFlTPJ1VbAW3MyMyUSRi/0yzNvoD6c99DyYX0KHFDWOzXhDThOAS
• f23idwmKLUFJPnqzI1vi3pST1+bpp/7Ob+x8mFYnVreQrCtg/gXru45B6wARAQAB
• tFRMYW1icmF0ZSBMaW51eCAoQ2hpYXZlIHVzYXRhIHBlciBpbCBzaXRvIGxhbWJy
• YXRlbGludXgub3JnKSA8aW5mb0BsYW1icmF0ZWxpbnV4Lm9yZz6JAlIEEwEIADwW
• IQTX07u4tbjclEdEblYbqVtQvG21rgUCYgEWCAIbAwULCQgHAgMiAgEGFQoJCAsC
• BBYCAwECHgcCF4AACgkQG6lbULxtta4s0xAA43xYBj4qONjoKOXqlUsv9iNP3C5a
• 9BOhbmpRR3HT8k15XUfPOk4Mqdzx8lHXR5pNyyMfAbbEewvMP9iWtuRptNtUvqAs
• 832lKEOLGVZujUi+pdDaScydXxVYuCUYuSTT+IE2yy8Siud8elhFR/t+r9Jfj+SR
• LWvXJeJtY8InIQugdn84GtECVTzxYhjveYmjAFwKuAC4rZglAnJKBkyTt6g1nLf3
• 5+1OlTpLL3xP910YPTveTkc0a3Hjoz7Z0CYzMUJW5C6ECdolU1rs07gIePipqsfc
• vNGn1eh0Sy0Fr9cmNfp7upTBUAe0AHfdsDATBTjEupTh5zzv/giMkLDblQObp+RB
• 2k9hvi6i+6wOVGGEJs0aAV9aEMtjGRwadNe73Ni8FwRj3Lqa/S2zif/TDlW/HFHC
• ccIsiA+b7U2U5soGWLBX+OhH/aDdSm7MNznbHTS/RWeELJYAMiQ8uWxNWOWiphUW
• EfK3MH6R3a4lUNxGjBtk2oxWZLtB4xOXLflFkMQxHFOleVyM06AMEoqxm/1yWaFJ
• PCffYd33+c787upVokUM1wh6tA9lPuD8K8zdJbaFz+CAztYbD2BO8F75LEXZSEWk
• 1Bresz7BNMsFhpNQGT45JgFBmpBLCJMI3bMWF11eUwS2UP/a5ICcoF8pQgM6Itil
• rxrDNm7tIkuvju+5Ag0EYgEWCAEQAOGbBb7pUNR7GCrbIomhjRa/2PEIhgGGmvXH
• YaCNdUtdjc6jDAtwdTzX5Vwt7Zgz3otNrqV+c13nLpo7LuQFrgnTK1S5IIuo7nF0
• f/qES8+r0umkRfFxmLNvhcdeEjQ9SuNr0r9rVz5LF9OHrb97Wte3G3RVLHCBP0SL
• 5S7iXIS/TWt+r7w+imWvulZBBi4Wx8w1sZ1X91fnyt50LXJ3m2e5LASl2N784yCs
• dSuqiSA8+ewWc+CAt4BzaXFvWFMJ0rFa7/lyJmYE0VukZKQj/XhsheRim0hVJV6S
• g2kRB27CJmUS/XdIBa7HkvHq6MwZoH6kZvQftz3VhEErpjMH+gaJ5q4wHoBNdyOZ
• 80YD6WgqtF7l+hljQgKUCESkZ5hJ3q90vREoZbRO0iNkJld9vjGsbiamFQhzteUT
• vR9y/s4a5/YhdiItIIRcuB7CVKd2oRBCiI97UEMcdA3N7bg/Bi+PHE6+xarEe77k
• FhaNRW/EWT88GiEVzCpRsC5gfVcY0DMLWHSFQRN70YRoPiofOtY9dJHBQU7eboxo
• VVPOtUOKOk2uzlMpuoR7sjFZY9SgaGJ3krwL7/7URq6FNGgO9VYT9C7QFS8j7WGo
• HMyDgNtckwXV92hPjaJax5NY7EslBOjPs24/ET5NHxeC2EQJZ2zqXQ7xr6PMvLJm
• XIcg1y23ABEBAAGJAjYEGAEIACAWIQTX07u4tbjclEdEblYbqVtQvG21rgUCYgEW
• CAIbDAAKCRAbqVtQvG21rtzdD/90p3GdXa5g/OrlKVZ3K6hPzwXV7WeH0rvmjX2H
• upNW/HXq7pXEwjj9EIgBGBeMCpWxeTXh2tjIt9Qxfw9hdEW6ySv2mNjo7JAQo7kl
• A1Lr1iDyVpa0B7wNP8BgsS6RC/uvBwLWSdp5kcynymjkskZ72rECiiysBN+fVx2Q
• Hgg2xIn279+eUsT1AXjN2prPAMXantvu0FK7g5Wp18ozWsYWBnX1eKKStXNVlJKy
• aspYVMCryZPE2QITGgWlOUAKqYh9dx7458DfukLk9RpAhFltMgiIFB6Y7oqhHPzI
• nJ/u6ySMm0tcjDj5DvAznV8XMUytZwqTtxacm8GpNzpz2S2spIsAG10vChjbzAE9
• jmt+yz+babsRz7Eh7C7nAajnRj3k7XlbqcSOoHqI7vt4V4YCCO41BH5pPRaYra1J
• 19lkTh7SgCkQt9aUHEhj5z3ubIRES5IxxkbGcOOLibBxJaybTrsA9aQTNC4atzyu
• yKmWJElWjcNFWJNS+djO2EYG7fLlylD+q1r+b6DXBi4GVuI/Wuqs9xLCeZJgsdEV
• VO6MlPLujYG/VYTOptP9k6RgvBJO5WUxLhysVp7eukPkGdl00MnKVYfXR/eryxDt
• KD6eTyoeKzjp60LDlJ1fkbVNY3eBcaXZxcEdTzUesvi1v2o6akiTwRpRuWsbMsPL
• GgJR6A==
• =5ubm
• - -----END PGP PUBLIC KEY BLOCK-----
• -----BEGIN PGP SIGNATURE-----
• 
• iQIzBAEBCAAdFiEE19O7uLW43JRHRG5WG6lbULxtta4FAmIDoE4ACgkQG6lbULxt
• ta6mgg//TdlYKUXHiy9B6w0ng3p7LtyT168JFq4ssugdqaltbYOP9H7j9h2/1oVG
• 6GBwEiunSB9o2ns6S+GNy3+lOKF59HifN5D/f8Qhon196J52meAPn8rjhA0lh4MG
• OKc3l0s/2C4CI4dMVEzghpPiViP3VpOOgkg9WgUeyCMxQEIX65BT4ZQWjRYgv+1K
• i9cgpHE4dqZIOJAykheJXw/aUKLr++v3IWvIbBNPND5PVq3xrnfnTi+Qdq1K8xYd
• SFiiWZyu5e5SzFVoIu9wRBszxfjEjXQrv065EKviJ0dCjYgmA9wVcBxzC4BTA6BW
• QMNuSbN9xQcJ1dJVSkJogufByrBqoln/Ju29d37yWDD3qPSFe+8Gu6qCGOQtJJaO
• ewHx6EzKBe3Y9dLP6/ZXsuQEr5T2R12EwzZW3YUorBV0YAFJ5dDM9rEh+W7VZNuw
• VIwYecyra1HSsZRrxJozHWWXD0dNxIMyVIIofd6KuJxfrhpuQqKpQnVvss764I9N
• lVIvtgxXdRmxd1n7MeQxbfR7L1viE9DtpB0vY5fw9ETC6y19s4ib4dphEEdo/7Z+
• LRWoEKBbcTpHxfEyqc7sC0Ol3xuAIgspRlj7BwGhSes47CSgGY/w0/COgyWJvEwd
• uc12vPB0wpMMkNKv3T6rvj92fKbKZHpz2GdBQrchMRN82QdU58Q=
• =4g24
• -----END PGP SIGNATURE-----
