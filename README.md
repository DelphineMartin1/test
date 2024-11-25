# test

#!/bin/bash

is_valid_user=false
is_valid_folder=false

#Création du nouvel usager
while [ "$is_valid_user" = false ]; do

	echo "Veuillez entrez le nom de l'utilisateur que vous souhaitez créer :"
	read USERNAME

	#Vérifier si déjà existant
	if [ id "$USERNAME" &>/dev/null ]; then
		echo "Erreur : Le nom d'utilisateur que vous avez entrez existe déjà.

	else
		is_valid_user=true
	fi

done

sudo useradd "$USERNAME"
echo "L'Utilisateur "$USERNAME" a été créé."


#Creer un répertoire pour l'utilisateur
while [ "$is_valid_folder" = false ]; do

	echo "Un répertoire va être créé, veuillez choisir un nom pour ce répertoire :"
	read FOLDER_NAME

	if [ -d "$FOLDER_NAME" ]; then
		if [ -z "$FOLDER_NAME" ]; then
			echo "Le répertoire ne peut pas avoir un nom vide."
		fi

		if [ -d "$FOLDER_NAME" ]; then
			echo "Un répertoire avec le nom \"$FOLDER_NAME\" existe déjà."
		else
			mkdir -p "$FOLDER_NAME"
			echo "Répertoire $FOLDER_NAME a été crée avec succès."
			is_valid_folder=true
		fi
	else
		mkdir -p "$FOLDER_NAME"
		echo "Répertoire $FOLDER_NAME a été crée avec succès."
		is_valid_folder=true
	fi
done

chmod +t "$FOLDER_NAME"
chmod 700 "$FOLDER_NAME"

#Afficher contenu fichier (cat)
FICHIER="README.txt"
touch FICHIER

echo "Bienvenue $USERNAME sur ton nouveau poste de travail." > "$FICHIER"

#Mettre l'adresse ip récupéré dans une variable
IP=$(hostname -I | awk '{print $1}')
echo "L'adresse IP de la machine : $IP" >> "$FICHIER"
cat "$FICHIER"
