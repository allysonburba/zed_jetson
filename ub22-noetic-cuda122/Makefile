build:
	docker build -t jetson2204-noetic .
#	 docker build -t personalroboticsimperial/prl:jetson2204-noetic . 

run:
	@docker container stop jetson24noetic || true && docker container rm jetson24noetic || true
	docker run \
		-it \
		-e "DISPLAY" \
		-e "QT_X11_NO_MITSHM=1" \
		-e "XAUTHORITY=${XAUTH}" \
		-e ROS_MASTER_URI \
		-e ROS_IP \
		-v ~/.Xauthority:/root/.Xauthority:rw \
		-v "/tmp/.X11-unix:/tmp/.X11-unix:rw" \
		--network host \
		--privileged \
		--runtime=nvidia \
		--name jetson24noetic \
		jetson2204-noetic
#		personalroboticsimperial/prl:jetson2204-noetic

# push:
# 	docker push personalroboticsimperial/prl:jetson2204-noetic