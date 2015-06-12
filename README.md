/*BIOINFORMATICA-I
Programa Creado el Java - Gerardo Rangel, Orson Mestanza. 
Este programa permite editar en el encabezado fasta o multifasta de las secuencias descargadas del NCBI.
Reemplaza los espacios vacios por "_" y ademas filtra las secuencias en base a una cadena de interes*/




import java.io.*;
public class Secuencias{
    public static void main(String args[]) {

        String linea, lectura="", nombreSinEspacios;

        FileReader fr = null;
        BufferedReader br = null;

        FileWriter fichero = null;
        PrintWriter pw = null;

        for(int j = 0; j < 17; j++){
            try{
                nombreSinEspacios = args[j].substring(0,args[j].lastIndexOf(".")); // el nombre sin espacios

                fr = new FileReader(new File(args[j]));
                br = new BufferedReader(fr);

                fichero = new FileWriter(new File(nombreSinEspacios + "_O.txt"));
                pw = new PrintWriter(fichero);

                linea = br.readLine(); 

                while(linea != null){
                    
                    if(linea.contains(">") && linea.contains(nombreSinEspacios)){

                        String[] temp = linea.split(" "); 
                        lectura = temp[0];
                        for(int i = 1; i < temp.length; i++){
                            lectura = lectura + "_" + temp[i];
                        }
                        pw.println(lectura);

                        linea = br.readLine();
                        while(!linea.contains(">")){
                            pw.println(linea);
                            linea = br.readLine();
                        }                        
                    }else{
                        linea = br.readLine();
                    }
                }

                fr.close();
                fichero.close();

            }catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
