# dropboxpython

# El folder esta en la carpeta de aplicaciones 

import dropbox


dbx = dropbox.Dropbox("TOKEN")
result = dbx.files_list_folder("/Folder", recursive=True)
lista_archivos = []

def funcionobtenerentradas(entries):
    for entradas in entries:
        if isinstance(entradas, dropbox.files.FileMetadata):
            lista_archivos.append(entradas.name)
            enlace = dbx.sharing_create_shared_link('/Folder/'+entradas.name).url #here i get the link shared
            print("Link created: ", enlace)

funcionobtenerentradas(result.entries)

while result.has_more:
    result = dbx.files_list_folder_continue(result.cursor)

    funcionobtenerentradas(result.entries)

print(len(lista_archivos))

