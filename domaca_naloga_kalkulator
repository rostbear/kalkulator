def preveri_stevila_v_izrazu(racun):
    #Preveri če izraz ima števila
    stevilo_stevilki = 0
    for char in racun:
        if char in ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']:
            stevilo_stevilki += 1
    if stevilo_stevilki == 0:
        print("Napaka: v izrazu niso prisotne številke!")
        return 1
    return 0


def preveri_pravilnost_stevila(racun):
    #Preveri, če izraz ima samo eno decimalno piko in števila
    stevilo_dec = 0
    stevilo_stevilki = 0
    for char in racun:
        if char in ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']:
            stevilo_stevilki += 1
        elif char == '.':
            stevilo_dec += 1
    if stevilo_stevilki == 0:
        print("Napaka: v izrazu niso prisotne številke!")
        return 1
    if stevilo_dec > 1:
        print("Napaka: v številki je prisotna vec kot ena decimalna pika!")
        return 1
    return 0


def preveri_simbole_in_stevilke(racun):
    #Preveri če izraz ima samo števila, decimalno piko in dovoljene simbole
    for char in racun:
        if char not in ['+', '-', '*', '/','^','(', ')', '.', '1', '2', '3', '4', '5', '6', '7', '8', '9', '0']:
            print("Napaka: v izrazu so prisotni nedovoljeni karakteri!")
            return 1
    return 0

def preveri_oklepaje(racun):
    #Preveri če je prvi oklepaj zaprt
    prvi_oklepaj = ''
    for char in racun:
        if char == '(' or char == ')':
            prvi_oklepaj = char
            break
    if prvi_oklepaj == ')':
        print("Napaka: prvi oklepaj v izrazu je zaprt!")
        return 1
   
    #Preveri odprte in zaprte oklepaje
    stevilo_odprtih_oklepajev = 0
    for char in racun:
        if char == '(':
            stevilo_odprtih_oklepajev += 1
        if char == ')':
            stevilo_odprtih_oklepajev -= 1
    if stevilo_odprtih_oklepajev != 0:
        print("Napaka: število odprtih in zaprtih oklepajev ni enako!")
        return 1
    return 0

#Pretvorimo podatke, ki vpišemo v parameter v tabelo z številkami in operacijami
def analiza(racun):
    tabela_izraza = []

    
    #Preveri če izraz ima števila
    error = preveri_stevila_v_izrazu(racun)
    if error > 0:
        return tabela_izraza, error

    #Preveri če je izraz pravilen
    error = preveri_simbole_in_stevilke(racun)
    if error > 0:
        return tabela_izraza, error
    
    #Preveri oklepaje
    error = preveri_oklepaje(racun)
    if error > 0:
        return tabela_izraza, error
    
    trenutni_simbol = ''
    #Dodamo zunanje oklepaje okoli računa
    racun2='('+ racun + ')'
    #Iteriramo vsak karakter
    for char in racun2:
        #Če je karakter številka ali decimalna pika, nam program karakter združi s predhodnimi v spremenljivki trenutni_simbol
        if char.isdigit() or char == '.':
            trenutni_simbol += char
        #Če karakter ni številka, pretvori trenutni_simbol v številko in jo doda v tabelo tabela_izraza
        else:
            if trenutni_simbol:
                #Preveri pravilnost števila
                error = preveri_pravilnost_stevila(trenutni_simbol)
                if error > 0:
                    return tabela_izraza, error
                else:
                    tabela_izraza.append(float(trenutni_simbol))
                    trenutni_simbol = ''
            #Če je karakter operacija, jo doda v tabelo tabela_izraza
            if char in ['+', '-', '*', '/','^','(', ')']:
                tabela_izraza.append(char)
    #V primeru, da je vpisana številka zadnja, program pretvori trenutni_simbol v številko in jo doda v tabelo tabela_izraza
    if trenutni_simbol:
        #Preveri pravilnost števila
        error = preveri_pravilnost_stevila(trenutni_simbol)
        if error > 0:
            return tabela_izraza, error
        else:
            tabela_izraza.append(float(trenutni_simbol))
        
    #Preveri dvojne simbole
    for i in range(len(tabela_izraza)-1):
        if tabela_izraza[i] in ['+', '-', '*', '/','^'] and tabela_izraza[i+1] in ['+', '-', '*', '/','^']:
            print("Napaka: dvojna računska operacija!")
            return tabela_izraza, 1
        
    #Preveri simbol pred oklepajem
    for i in range(len(tabela_izraza)-1):
        if tabela_izraza[i] not in ['+', '-', '*', '/','^','(', ')'] and tabela_izraza[i+1] in ['(']:
            print("Napaka: število namesto operacije pred oklepajem!")
            return tabela_izraza, 1

    #Preveri simbol za oklepajem
    for i in range(len(tabela_izraza)-1):
        if tabela_izraza[i] in [')'] and tabela_izraza[i+1] not in ['+', '-', '*', '/','^','(', ')']:
            print("Napaka: število namesto operacije za oklepajem!")
            return tabela_izraza, 1
        
    #Preveri simbol pred zaprtim oklepajem
    for i in range(len(tabela_izraza)-1):
        if tabela_izraza[i] in ['+', '-', '*', '/','^'] and tabela_izraza[i+1] ==')':
            print("Napaka: Operacija pred zaprtim oklepajem!")
            return tabela_izraza, 1
        
    #Preveri prazne oklepaje
    for i in range(len(tabela_izraza)-1):
        if tabela_izraza[i] == '(' and tabela_izraza[i+1] == ')':
            print("Napaka: v oklepajih manjka izraz!")
            return tabela_izraza, 1

    #Nam vrne tabelo z številkami in operacijami
    return tabela_izraza, 0

#Program izračuna izraz iz tabele tabela_izraza 
def lahek_racun(tabela_izraza):
    #Računa potenco, če je simbol med številima "^"
    while '^' in tabela_izraza :
        #Poišče pozicijo simbola "^" v tabeli tabela_izraza
        for i in range(len(tabela_izraza)):
            if tabela_izraza[i] == '^':
                operator = tabela_izraza[i]
                operand1 = tabela_izraza[i - 1]
                operand2 = tabela_izraza[i + 1]
                #Izračuna rezultat kot potenco števila pred in števila za simbolom "^"
                result = operand1 ** operand2
                #Skrči elemente v izrazu z rezultatom
                tabela_izraza[i - 1:i + 2] = [result]
                break
    #Računa množenje ali deljenje, če je simbol med številima "*" ali "/"  
    while '*' in tabela_izraza or '/' in tabela_izraza :
        #Poišče pozicijo simbola "*" ali "/" v tabeli tabela_izraza
        for i in range(len(tabela_izraza)):
            if tabela_izraza[i] in ['*', '/']:
                operator = tabela_izraza[i]
                operand1 = tabela_izraza[i - 1]
                operand2 = tabela_izraza[i + 1]
                #Izračuna rezultat kot produkt ali količnik števila pred in števila za simbolom "*" ali "/"
                if operator == '*':
                    result = operand1 * operand2
                else:
                    #Preveri če je prisotno deljenje z ničlo
                    if operand2 == 0:
                        print("Napaka: v izrazu je prisotno deljenje z ničlo!")
                        return 0, 1
                    else:
                        result = operand1 / operand2
                #Skrči elemente v izrazu z rezultatom
                tabela_izraza[i - 1:i + 2] = [result]
                break
    #Računa seštevanje ali odštevanje, če je simbol med številima "+" ali "-"  
    while '+' in tabela_izraza or '-' in tabela_izraza:
        #Poišče pozicijo simbola "+" ali "-" v tabeli tabela_izraza
        for i in range(len(tabela_izraza)):
            if tabela_izraza[i] in ['+', '-']:
                operator = tabela_izraza[i]
                operand1 = tabela_izraza[i - 1]
                operand2 = tabela_izraza[i + 1]
                #Izračuna rezultat kot vsoto ali razliko števila pred in števila za simbolom "+" ali "-"
                result = operand1 + operand2 if operator == '+' else operand1 - operand2
                #Skrči elemente v izrazu z rezultatom
                tabela_izraza[i - 1:i + 2] = [result]
                break
    #Vrne nam prvi in edini element tabele tabela_izraza
    return tabela_izraza[0], 0

#Funkcija nam vrne izraz med zadnjim odprtim in prvim naslednjim zaprtim oklepajem
def isci_oklepaj(tabela):
    #Inicializira pozicijo odprtega in zaprtega oklepaja
    start=0
    end=0
    #Inicializira flag, ki nam pove, če je odprti oklepaj najden
    start_dob=False
    #Iterira tabelo 
    for i in range(len(tabela)):
        #Če je iteriran simbol "(", postavi njegovo pozicijo v start in flag se inicializira na True
        if tabela[i]=='(':
            start=i
            start_dob=True
        #Če je iteriran simbol ")", postavi njegovo pozicijo v end in flag se inicializira na False
        else:
           if tabela[i]==')'and start_dob:
               end=i
               start_dob=False
            
    #Postavi izraz med oklepaji v tabelo tabela_pom
    tabela_pom=tabela[start+1:end]
    racun=0
    #Če je prvi simbol v tabeli tabela_pom + ali -, pomnoži prvo številko s (+1) ali (-1)
    if tabela_pom[0] in ['+', '-']:
        if tabela_pom[0] == '-':
            tabela_pom[1]=tabela_pom[1]*(-1)
        #Izračuna izraz v tabeli tabela_pom in ga postavi v spremenljivko racun
        racun, error=lahek_racun(tabela_pom[1:])
        #Proveri če so prisutne napake
        if error > 0:
            return tabela, error
    else:
        #Izračuna izraz v tabeli tabela_pom in ga postavi v spremenljivko racun    
        racun, error=lahek_racun(tabela_pom)
        if error > 0:
            return tabela, error
    
    #Skrči izračunan izraz v rezultat
    tabela[start:end+1]=[racun]
    #Vrne nam tabelo
    return tabela, 0
#Izračuna celoten izraz
def popolni_racun(tabela):
    #Inicializira tabelo 2 s tabelo
    tabela2=tabela
    #Dokler tabela2 ima več kot 1 element, program izračuna izraz v zadnjih oklepajih v tabeli in skrči tabelo
    while len(tabela2)>1:
        tabela2, error=isci_oklepaj(tabela)
        #Proveri če so prisutne napake
        if error > 0:
            return 0, error
    #Vrne nam prvi in edini element v tabeli
    return tabela2[0], 0
    
#Glavni program:    
while True:
    #Vpraša uporabnika, da vpiše račun
    user_input = input("Vtipkaj nek račun: ")
    #Razbije račun v tabelo
    tabela_izraza, error = analiza(user_input.replace(" ", ""))
    #Proveri če niso prisutne napake
    if error == 0:
        #Če je izraz tipa a/b, nam bo program vrnil rezultat brez decimalk in ostanek
        if len(tabela_izraza)==5 and tabela_izraza[2]=='/':
            if tabela_izraza[3] ==0:
                 print("Napaka: v izrazu je prisotno deljenje z ničlo!")
            else: 
                print("Rezultat je:", int(tabela_izraza[1]/tabela_izraza[3]), "Ostanek je: (", tabela_izraza[1]%tabela_izraza[3], ")")
        #Drugače se program izpelje navadno
        else:
            #Izračuna celoten izraz
            finalna_tabela, error = popolni_racun(tabela_izraza)
            #Preveri če so prisotne napake
            if error == 0:
                #Napiše rezultat
                print("Rezultat je:", tabela_izraza[0])
