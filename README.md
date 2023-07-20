# Torrent-esque P2P File-sharing System Assignment
From SNU ECE 2022 & 2023 Fall **Introduction to Data Communication Networks** class. 

## Program Specification

In this assignment, you will implement a torrent-esque P2P file sharing system. This system defines a
custom network protocol for file sharing. You must implement the said protocol.

Our torrent system partitions a file into blocks and distributes them to peers. The torrents are
referenced using a hash value of the file in our torrent network. Management of the torrent
information and data is not the focus of this assignment. What you will be implementing is the
custom network protocol of our torrent network. You will create a working torrent program that can
communicate with the model implementation of our torrent network, at the end of this assignment.

Our custom network protocol is implemented as follows:
- A peer first requests torrent info from a seeder using the hash value of the torrent, using
REQUEST_TORRENT command.
- The seeder responds with the torrent info, using the PUSH_TORRENT command. The requester
receives the torrent info, creates a new torrent_file struct and adds it to its global torrent list. (Refer
to torrent_functions.h) The seeder is also added to the peer list of the new torrent.
- The requester requests block info of the seeder using the REQUEST_BLOCK_INFO command. The
seeder responds with the block info of the torrent, using the PUSH_BLOCK_INFO command.
- With the block info of the seeder, the requester can now check which block the seeder has. The
requester then requests its missing blocks from the seeder using the REQUEST_BLOCK command. The
seeder responds with the requested block, using the PUSH_BLOCK command.
- At random intervals, the requester can request a peer list from a random peer(seeder) using the
REQUEST_PEERS command. The random peer responds with its peer list of the torrent, using the
PUSH_PEERS command. This way, the requester can discover new peers of the torrent.
- The requester can also request block info of the newly discovered peer using
REQUEST_BLOCK_INFO command, and request missing blocks from those new peers using
REQUEST_BLOCK command.
- Of course, being a P2P system, any requester can also act as a seeder, and any seeder can also act
as a requester.

The requester routines are managed in client_routines() function, while the seeder routines are
managed in server_routines() function. Please refer to the comments in main.c, network_functions.h,
torrent_functions.h and the code structure of the skeleton code for more details.

The Skeleton code is provided in the assignment tab of ETL. Copy the code to your system (WSL,
MacOS, Ubuntu, etc.), and modify main.c to complete your assignment.

**Note: A more detailed explanation of the assignment can be found in the main.c file.
Please read the explanation in main.c file CAREFULLY before starting your assignment!**
