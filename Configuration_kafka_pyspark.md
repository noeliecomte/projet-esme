# Configuration kafka et pyspark

Ce projet contient les étapes pour configurer un environnement de streaming de données en temps réel utilisant Apache Kafka et Apache Spark.

## Installation de Java

1. Mettre à jour les paquets :
   ```bash
   sudo apt-get update
   ```
2. Installer Java JDK 11 :
   ```bash
   sudo apt-get install openjdk-11-jdk-headless
   ```
3. Vérifiez l'installation :
   ```bash
   java --version
   ```

## Configuration de Java

1. Ajouter Java à votre variable d'environnement :
   ```bash
   echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> ~/.bashrc
   echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
   source ~/.bashrc
   ```

## Installation de Kafka

1. Téléchargez et extrayez Kafka :
   ```bash
   wget https://archive.apache.org/dist/kafka/2.6.0/kafka_2.12-2.6.0.tgz
   tar -xzf kafka_2.12-2.6.0.tgz
   ```

## Lancement de Zookeeper et Kafka

1. Lancer Zookeeper :
   ```bash
   ./kafka_2.12-2.6.0/bin/zookeeper-server-start.sh ./kafka_2.12-2.6.0/config/zookeeper.properties
   ```
2. Lancer Kafka :
   ```bash
   ./kafka_2.12-2.6.0/bin/kafka-server-start.sh ./kafka_2.12-2.6.0/config/server.properties
   ```

## Création d'un Topic Kafka

1. Créer un topic nommé :
   ```bash
   ./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic tp-meteo
   ```

## Installation de Spark (Personnalisation requise)

1. Téléchargez et extrayez Spark :
   ```bash
   wget https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop2.7.tgz
   tar -xvf spark-3.2.3-bin-hadoop2.7.tgz
   ```
2. Configurez Spark :
   Remplacez "tp-esme" par le nom de votre répertoire.
   ```bash
   export SPARK_HOME=/workspaces/<votre-repertoire>/spark-3.2.3-bin-hadoop2.7
   export PATH=$SPARK_HOME/bin:$PATH
   ```

## Installation de Python 3.10

1. Mettre à jour Python :
   ```bash
   sudo apt update
   sudo apt install -y python3.10 python3.10-venv python3.10-distutils
   ```
2. Installer la bibliothèque `python-kafka` :
   ```bash
   python3.10 -m pip install kafka-python
   ```

## Exécution des Scripts

1. Exécuter le producteur Kafka `producer.py` avec Python 3.10 :

   ```bash
   python3.10 producer.py
   ```

2. Exécuter le script Spark `spark.py` :

   ```bash
   $SPARK_HOME/bin/spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.3 spark.py
   ```
