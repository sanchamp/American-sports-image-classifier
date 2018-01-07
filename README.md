Steps to Run.

1. intall tensorflow
2. clone this repository
3. Download and prep the dataset by downloading the image and storing the based on their classes. eg.
ls tf_files/players_photos
The preceding command should display the following objects:
nba players/
nfl players/

4. Launch Tensorboard for monitoring and inspection
tensorboard --logdir tf_files/training_summaries &

5. Run the retrain script
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=1000 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"mobilenet_0.50_224" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="mobilenet_0.50_224" \
  --image_dir=tf_files/players_photos

  python -m scripts.retrain --bottleneck_dir=tf_files/bottlenecks --how_many_training_steps=1000 --model_dir=tf_files/models/ --summaries_dir=tf_files/training_summaries/"mobilenet_0.50_224" --output_graph=tf_files/retrained_graph.pb --output_labels=tf_files/retrained_labels.txt --architecture="mobilenet_0.50_224" --image_dir=tf_files/car_photos  

6. Test the network by classifying a new image
python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/test_data/img1.jpg

7. Notes on Improvements
Manipulate the parameters in the retain script for higher accuracy or faster training time eg.
Reduce the --learning_rate in the retrain script from 0.01 to 0.005 for higher accuracy
