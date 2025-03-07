# Code of your exercise

```java
@Override
    public void visit(ClassOrInterfaceDeclaration declaration, Void arg) {
        for(FieldDeclaration method : declaration.getFields()) {
            if (method.isPrivate()) {
                if(hasGetter(declaration, method.getVariable(0).getNameAsString()))
                {
                    writeToFile("code/Exercise4/Result.md", "This field is private and has no getter: " +method.getVariable(0).getTypeAsString() + " " +  method.getVariable(0).getNameAsString() +  "\n"
                    + " Package : " + declaration.getFullyQualifiedName().orElse("[Anonymous]")  + "\n" 
                    + " Class : "+ declaration.getNameAsString() + "\n" + "\n");
                }
                else{
                    writeToFile("code/Exercise4/Result.md","This field is private but has a getter : " +method.getVariable(0).getTypeAsString() + " " +  method.getVariable(0).getNameAsString() +  "\n"
                    + " Package : " + declaration.getFullyQualifiedName().orElse("[Anonymous]") + "\n" 
                    + " Class : "+ declaration.getNameAsString() + "\n" +"\n");
                }
                
            }
        }
        visitTypeDeclaration(declaration, arg);
    }

     private static boolean hasGetter(ClassOrInterfaceDeclaration clazz, String fieldName) {

        String getterName = "get" + fieldName.substring(0, 1).toUpperCase() + fieldName.substring(1); 
            
        return clazz.getMethodsByName(getterName).stream().anyMatch(methodDeclaration -> !methodDeclaration.getType().asString().equals("void"));
    }

    private static void writeToFile( String fileName, String content ) {
        try {
            // Création d'un objet File pour le fichier Markdown
            File file = new File(fileName);

            // Création du FileWriter pour écrire dans le fichier
            FileWriter fw = new FileWriter(file,true);

            // Création du BufferedWriter pour une écriture plus efficace
            BufferedWriter writer = new BufferedWriter(fw);

            // Écriture du contenu dans le fichier Markdown
            writer.write(content);

            // Fermeture du BufferedWriter
            writer.close();

            System.out.println("Les informations ont été écrites dans le fichier " + fileName);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

### Result :
