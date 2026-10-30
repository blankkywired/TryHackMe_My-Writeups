# Downloading Files
**Wget:**
 Usado para transferencia de arquivo de um site web através do protocolo http
 image.pngimage-1.png
No laboratório iniciamos a instancia da maquina vulneravel com a vpn para nos conectarmos a mesma rede para possibilitar o ataque(Ataccker <--> Machine)
**Usei o comando ping para checar a conexão com a maquina atacada**
 Posteriormente usei o comando

    ```
    tryhackme@linux3:~$ python3 -m http.server 8000
    ```
- para iniciar um servidor python http (SimpleHTTPServer) dentro da maquina vulnerável
- Na minha maquina atacante realizei o scaneamento da vitima usando o comando nmap -sV <MACHINE_IP> ![](https://remnote-user-data.s3.amazonaws.com/OPOuVPKF9JVRSUZihnyeY9O4Ihek01ZTV8tTN6ua1RjchaHD_5D1_3Tzgg44c2JjREJwIPGPcvcSuRgYPEhPQ9c_qvPO1aPmkOq32gzqm6cgjSwq7AypqbXrxucNcWb2.png)
- Após isso confirmei que realmente a maquina estava rodando o servidor http na porta 8000
- Observação: Cada serviço pode ser aberto em qualquer porta, por isso o servidor http apresenta a porta 8000, a porta 80 é so um padrão porta logica de serviço, mas não é obrigatorio
 Com o servidor iniciado podemos executar o comando wget para obter a flag

**Question**: Download the file [http://MACHINE_IP:8000/.flag.txt](http://MACHINE_IP:8000/.flag.txt) onto the TryHackMe AttackBox. Remember, you will need to do this in a new terminal.
 What are the contents?
 Para baixar o arquivo do servidor para minha maquina utilizei o comando wget
 
 A estrutura do comando wget é basicamente a seguinte:

    ```
        tryhackme@linux3:/tmp# wget http://MACHINE_IP:PORT/file     
    ```

    ```
    ┌──(kali㉿kali)-[~]
    └─$ wget http://10.66.148.145:8000/.flag.txt
    ```
- após baixar o arquivo do servidor para a minha maquina, o arquivo ficou salvo na pasta do meu user, usando comando cat .flag.txt para exibir a flag
 

# Process 101
**Question**: If we were to launch a process where the previous ID was "300", what would the ID of this new process be?
 R: Os processos do Linux são organizados por ordem enumeradas a partir do número 1
 Se um processo anterior tinha PID (Process ID) 300 Então o ID do novo processo será 301
 Usamos o comando ps para checar a lista de processos 
 ![](https://remnote-user-data.s3.amazonaws.com/42jzsn9Qfom8SFChGpnuuLkV72KG5fHsYLXZX2o84s8mzwxu6CgVlGF1a7CeIJES0CZhVB8dqcq2YR8-w4UI3xv9iqaFbqP6Om7_UZWo6hOUBe5ABiME0J6jSOPh1cTK.png)

**Question**: If we wanted to cleanly kill a process, what signal would we send it?

R: O comando usado para limpar o processo é SIGTERM

**Question**: Locate the process that is running on the deployed instance (MACHINE_IP). What flag is given?
- ![](https://remnote-user-data.s3.amazonaws.com/arWrnC6dHVlUz2b4GegyGlAzXyVniwS7Vcb5ZqcI4seYdgwh5qjYnxt-SrI6vMRhHjZvv6tRg0DG7GqPmFXjhEwpqAmbH2GhbD9rxswPs0G8NFl_lrGnVSba8dNJSdoB.png)

R: usando o  comando ps encontrei a flag do comando que estava sendo executado 

# Maintaning Your Sytem: Automation

 **Question**: When will the crontab on the deployed instance (10.67.181.6) run?
 R: Para ver a lista de crontabs que foram criados eu uso o comando:

    ```
    ┌──(kali㉿kali)-[~]
    └─$ crontab -e
    ```
- ![](https://remnote-user-data.s3.amazonaws.com/Q2VBF7sSCZprlL-eOTrTaOfVUUnQORDqW5-92o0O_kKEh3A8Ql5dBL8FlWpYCLScJZwDuhF3TqRD5vqZzVx2Pq-e5y9foJC4e4yzCEx2VeN9tz8xAfghNXHhBUZu1z76.png)
- O crontab da instancia <MACHINE_IP> vai rodar todas as vezes que o sistema reiniciar, assim executando o script processes.sh, sendo assim: @reboot

# Maintaning your system: Logs
 
**Question**: What is the IP address of the user who visited the site?

![](https://remnote-user-data.s3.amazonaws.com/xjsNNEq6066u75dvpgb6pGlY6ZOLSiHJOQqRN-Avo0IWbjJK8z2CvNg1AurE1GzVPxLGIm09_NP10nX3n-ONxTFxqSulZ_e6HCK6WvXVuWmpxn15pnMjovB-eOsisIej.png)

Para acessar os logs do server apache2  precisei entrar na pasta do sistema /var e apos isso procurar a pasta de logs e selecionar a pasta de logs do servidor apache, para isso utilizei o comando: 

    ```
    cd /var/log/apache2 
    ```
![](https://remnote-user-data.s3.amazonaws.com/yEQeQqOAl-_GMBLZkUKEf43WQWCiDzeUe6mTQinZLOEf_Hd2qTYO0CyvYoC45wLWDTXpKVolMvYTta-h2hBFvEqHF5F8VFlhpxhHobnAN7r6-sOeczRRaednBs7lcnOT.png)

![](https://remnote-user-data.s3.amazonaws.com/dnEVhweUVALaq2h1lxWxTjjJKnQLuTrbE-Lpo6dTgvELuVGf7BejUu2rczbhMX9_eRFsA_ZylKEpictkicV5k3lCSAlwDX_-Dz7gqHXx3L-0reYDZD7M7IgI96_TFjif.png)
Usando  o comando nano para visualizar o arquivo encontramos o IP do client que acessou o site
R: 10.9.232.111
**Question**: What file did they access?
![](https://remnote-user-data.s3.amazonaws.com/sT92p7L7FBwCWX4X8Y1CAodfu5C2GjJObcfncmH3A3SszwBGfuY_m7yiVb1GUa1VT7O7wSSiE68mTJFTvF1TqMB0mGgMqDyB9uVY7gaUqB_1WY8yQOA4Ezv37bAOjNxG.png)
R: catsanddogs.jpg
