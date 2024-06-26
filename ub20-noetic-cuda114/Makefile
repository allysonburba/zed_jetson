build:
	docker build -t personalroboticsimperial/prl:jetson2004-cuda114-noetic . 

run:
	@docker container stop jetson20noetic || true && docker container rm jetson20noetic || true
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
		--name jetson20noetic \
		personalroboticsimperial/prl:jetson2004-cuda114-noetic

# push:
# 	docker push personalroboticsimperial/prl:jetson2004-cuda114-noetic