CC = g++
CFLAGS = -std=c++11 -Wall

SRCS = kmeans-serial.cpp
OBJS = $(SRCS:.cpp=.o)
EXEC = kmeans

all: $(EXEC)

$(EXEC): $(OBJS)
	$(CC) $(CFLAGS) $(OBJS) -o $(EXEC)

%.o: %.cpp
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJS) $(EXEC)