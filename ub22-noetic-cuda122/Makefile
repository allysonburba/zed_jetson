build:
	docker build -t allysonburba/prl:jetson2004-cuda122-noetic .

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
		allysonburba/prl:jetson2004-cuda122-noetic

push:
	docker push allysonburba/prl:jetson2004-cuda122-noetic